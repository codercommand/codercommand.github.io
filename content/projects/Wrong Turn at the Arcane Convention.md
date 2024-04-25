+++
title = 'Wrong Turn at the Arcane Convention'
date = 2023-12-11
draft = false
+++

{{< youtube vA8ORlfA9V0 >}}

[itch.io page](https://tantandev.itch.io/forest-cleaner)

I had just finished reading the [Unofficial Bevy Cheat Book](https://bevy-cheatbook.github.io/) in December of 2023 because I was interested in trying the Bevy game engine at the time. I then saw a public discord message by Tantan looking for people to join him in a game jam using bevy and decided send a request.

I got accepted and worked on the game for ~3 days along with Tantan and another programmer called Mini. I worked on the camera movement code, refactored the project sturcture multiple times, created a code based prefab system for creating and spawning entities, and I made approximately 90% of all the AI systems in the game.

The AI system works by adding components to create unique AI behaviors. An example of this is the fire and mage/human enemies in the game. The Fire enemy uses ChasePlayer while the mage/human uses Archor which both control how they approach the player.

The AI system works by feeding data along in a chain with some components being swapable or having different starting/ending points in the imaginary chain. Example: Perception -> (ChasePlayer/Archer) -> MovementDirection. 

```rust
// Code snippet of fire enemies AI components
Name::new("enemy - fire element"),
Perception::new(90.0, 110.0),
MovementDirection::default(),
AttackInput::default(),
FireElement {
    timer: Timer::from_seconds(rng.gen_range(3..10) as f32, TimerMode::Once),
    attack_type_toggle: true,
},
ChasePlayer,
MeleeAttack {
    range: 20.0,
    timer: Timer::from_seconds(0.1, TimerMode::Once),
    strength: 1_000.0,
},
Roam {
    idle_chance: 0.0005,
    change_direction_chance: 0.001,
}
```

```rust
// Code snippet of human enemies AI components
Name::new("enemy - skilled mage"),
Knockback::new(0.9),
Perception::new(120.0, 160.0),
MovementDirection::default(),
Archer {
    range: 110.0,
    dead_zone: 10.0,
},
AttackInput::default(),
Roam {
    idle_chance: 0.0005,
    change_direction_chance: 0.001,
},
Weapons::default(),
WeaponRange(115.0),
```

```rust
// AI Code from chase_player.rs
use crate::*;
use bevy::prelude::*;

#[derive(Debug, Component)]
pub struct ChasePlayer;

pub fn chase_player_when_perceived(
    mut entities: Query<
        (&mut MovementDirection, &Perception, &Transform),
        (With<EntityCore<Enemy>>, With<ChasePlayer>),
    >,
    player: Query<&Transform, With<EntityCore<Player>>>,
) {
    if let Ok(player) = player.get_single() {
        for (mut move_direction, perception, transform) in entities.iter_mut() {
            if perception.is_tracking {
                let direction: Vec2 = player.translation.xy() - transform.translation.xy();
                **move_direction = direction.normalize_or_zero();
            }
        }
    };
}
```

```rust
// AI Code from archer.rs
use crate::*;
use bevy::prelude::*;

/// Archer takes a number representing how close they'll move to the player.
/// If the player gets to close, they'll move away in the opposite direction.
#[derive(Debug, Component)]
pub struct Archer {
    // How close it will allow the player to get before moving away.
    pub range: f32,
    // The tolerance amount added to the range where the AI won't bother moving toward or away from the player.
    // A value greater than 0 is require so entities don't move back and forth at the FPS rate.
    pub dead_zone: f32,
}

pub fn archer_movement(
    mut entities: Query<
        (&mut MovementDirection, &Archer, &Perception, &Transform),
        With<EntityCore<Enemy>>,
    >,
    player: Query<&Transform, With<EntityCore<Player>>>,
) {
    if let Ok(player) = player.get_single() {
        for (mut move_direction, archer, perception, transform) in entities.iter_mut() {
            let distance: f32 = player.translation.xy().distance(transform.translation.xy());
            let direction: Vec2 =
                (player.translation.xy() - transform.translation.xy()).normalize_or_zero();

            if perception.is_tracking && distance > (archer.range + archer.dead_zone) {
                **move_direction = direction;
            } else if perception.is_tracking && distance < archer.range {
                **move_direction = direction * -1.0;
            } else if perception.is_tracking {
                // Since the other conditions didn't run, we assume this is the dead zone.
                **move_direction = Vec2::ZERO;
            }
        }
    };
}
```