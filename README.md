# Comic-Con Parking System — Database Design

## Overview
ER diagram for a multi-zone event parking system covering vehicle tracking, spot allocation, ticketing, and payments across multiple event days.

## Key Design Decisions

**Zones and Levels are decoupled**: 
Both are independent entities. A parking spot links to a zone and a level directly via separate FKs rather than nesting one inside the other.

**Spot categories handle reserved parking**: 
VIP, Exhibitor, Staff, EV Charging, and Cosplayer spots are modeled via a separate `spot_categories` table linked to each parking spot.

**Sessions are the central structure**: 
One session = one visit. Entry time, exit time, vehicle, and assigned spot all live here. A NULL exit_time means the vehicle is currently inside.

**One vehicle, many sessions**: 
Vehicle identity is stored once. All visit history across days lives in `parking_sessions` via FK.

**Spot reuse over time**: 
The same spot can serve multiple vehicles over time. Current availability is tracked via `is_available` on `parking_spots`.

**Ticket and Payment are separate from Session**: 
Ticket is one-to-one with a session. Payment is also per session but kept separate to track status, mode, and timestamp independently.

See the `erd.png` for full diagram.
