---
title: Playanimation
category: Commands
mentions:
    - BedrockCommands
    - zheaEvyline
description: Some useful playanimation commands
---

## Introduction

[Sourced by the Bedrock Commands Community Discord](https://discord.gg/SYstTYx5G5)

In this page, we will look at some `/playanimation` commands that can be applied to almost any entity, making them versatile and useful for various scenarios.

Before diving into the commands, we recommend reviewing the [Minecraft Wiki Playanimation Command Guide](https://minecraft.wiki/w/Commands/playanimation) to understand the basics of how the command works.

## Syntax

`playanimation <entity: target> <animation: string> [next_state: string] [blend_out_time: float] [stop_expression: string] [controller: string]`

## List of Useful Playanimation Commands

- These commands can be applied to nearly any entity, including players.
- All variables are initialized as zero in the examples but can be adjusted as needed.
- Some commands use multiple variables. You can add or remove variables based on your requirements.
- Controller names (e.g., `wiki:body_yrot`) enable stacking animations without overwriting previous ones.  
    - You are free to change the namespace (`wiki`) or the controller names to your liking.

### Body Animations

1. Rotate the body of the entity along the Y-axis (excluding limbs and head):
    - `/playanimation @a animation.player.attack.rotations none 0 "v.attack_body_rot_y=0;" wiki:body_yrot`
2. Rotate the body of the entity along the Z-axis (excluding limbs and head):
    - `/playanimation @a animation.wolf.shaking none 0 "v.body_rot_z=0;" wiki:body_zrot`

### Root Animations

1. Rotate the entire entity along the X-axis and Z-axis:
    - `/playanimation @a animation.ender_dragon.setup none 0 "v.clamped_pitch=0;v.clamped_roll=0;" wiki:root_xrot_yrot`
2. Offset the entire entity's position along the X, Y, and Z axes:
    - `/playanimation @a animation.minecart.move none 0 "v.rail_offset.x=0;v.rail_offset.y=0;v.rail_offset.z=0;" wiki:root_pos`

### Head Animations

1. Offset or rotate the entity's head:
    - `/playanimation @a animation.ender_dragon.neck_head_movement none 0 "v.head_position_x=0;v.head_position_y=0;v.head_position_z=0;v.head_rotation_x=0;v.head_rotation_y=0;v.head_rotation_z=0;" wiki:head_pos_rot`
