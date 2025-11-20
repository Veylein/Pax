# Discord Chi Bot 🐼

## Overview
The Discord Chi Bot gamifies positive user interactions within a Discord community by tracking "chi" (positive energy), assigning roles, and offering rewards for desirable behavior, while actively discouraging negative language. Its core purpose is to foster a positive community environment through gamified social interactions. Key features include a monthly quest system, a turn-based PvP duel system with spectator betting, team functionalities with base activities, an artifact system with trading, a comprehensive pet management system with combat and training, a chi-based farming system (gardens), and a web-based administrative panel.

## User Preferences
- **Admin Code**: `Panda-Gang-Community-2025`
- **Clean Restarts**: Discord bot disconnects and reconnects gracefully when Replit restarts
- **Showcase Ready**: Bot prepared for Discord YouTuber demonstrations with all features tested and working

## Recent Changes (November 15, 2025)
- **🎯 Major Simplification - Dongtian Removed**: Removed entire Winter Wonderland (Dongtian) world system (1,775 lines) due to user confusion. Bot now focuses on single-world simplicity with streamlined gameplay
- **🌍 Universal Deployment**: Removed all server-specific channel restrictions. Bot now works on ANY Discord server in ANY channel - duels, training, and combat are no longer locked to specific channels
- **⚙️ Enhanced P!setup Command**: Auto-creates all required infrastructure including Positive Chi, Negative Chi, and Quest Completer roles with proper colors, plus auto-creates panda-bot-logs event channel with correct permissions
- **🏆 Achievement Cleanup**: Removed 3 Dongtian-related achievements (Winter Wanderer, Winter Explorer, Frost Conqueror) to align with simplified single-world design
- **Garden Bundle System**: Complete bundle purchasing system with **P!bundle** to view 3 premium garden bundles (Sickle Bundle 75k chi, Heroic Bundle 60k chi, Scythe Bundle 40k chi)
- **Garden Economy Rebalance**: Gardens balanced at 40% baseline yield to prevent chi inflation while maintaining viable ROI (8-10%)
- **Garden Tool System**: Comprehensive crafting system with 9 unique tools across 4 tiers (Basic +10%, Advanced +20-25%, Elite +35%, Mythic +50%)
- **Player Shop System**: Complete player-to-player marketplace with 8 commands (create, sell, buy, search, list, view, remove, stats)
- **P!say Command**: Bot repeats user text with automatic message deletion for clean announcements
- **All Features Fully Functional**: Showcase-ready for Discord YouTubers with simplified, universally deployable design

## System Architecture

### Main Components
The system consists of a Discord bot (`main.py`), a FastAPI backend (`api.py`), and a React frontend (`dashboard/`), all managed by `run.py` using uvicorn. Data is persistently stored in a PostgreSQL database via an async-safe service layer.

### UI/UX Decisions
- **Discord Interactions**: Employs rich embeds for information display (e.g., leaderboards, quest announcements), emoji reactions for user feedback, and interactive buttons for seamless feature access.
- **Landing Page**: A static HTML page serves as a simple landing page.

### Technical Implementations
- **Chi System**: Monitors messages for sentiment, assigns/deducts chi with cooldowns, includes user blacklists, a unified rebirth system (500k chi threshold, incremental), daily role assignments, and random chi events. The economy is balanced for scarce, valuable chi.
- **Quest System**: Features tutorial quests for new users and seasonal monthly themed quests with increasing rewards.
- **Shop Systems**: Includes separate Rebirth and Chi Shops, an inventory system with categorized displays, and numbered item identifiers. Player Shop System allows users to create their own shops with unique IDs (S1, S2, etc.), list items from inventory with custom prices, and conduct secure chi-based transactions. Features comprehensive search, shop browsing, sales tracking, and automatic seller notifications.
- **Dueling System**: Turn-based PvP combat with item usage, HP tracking, spectator betting, and an item upgrade system.
- **Boss & NPC Combat**: PvE turn-based combat against unique bosses and solo training against AI opponents with varying difficulty.
- **Town System**: Expandable system featuring Panda Town and Lushsoul Cavern with shops and mining.
- **Team System**: Supports team creation, management, base customization, upgrades, score tracking, and alliance/enemy mechanics.
- **Artifact System**: Randomly spawning, tiered artifacts that are claimable, usable for healing, and tradable.
- **Pet System**: Redesigned system with 5 unique pets (Ox, Snake, Tiger, Panda, Dragon), each with 3 special attacks and garden enhancement bonuses. Includes pet purchasing, info, switching, feeding, and a pet food system. A framework for pet evolution and turn-based pet battles is prepared.
- **Garden System**: A chi-based farming system with three upgradeable tiers, featuring planting, growth timers, watering, chi harvesting, and a fertilizer mechanic. Includes comprehensive tool system with 9 unique tools across 4 tiers (Basic +10%, Advanced +20-25%, Elite +35%, Mythic +50%) that provide percentage harvest bonuses, growth speed bonuses, and flat chi bonuses. Tools can be purchased (Chi Shop), crafted (artifacts+ores via P!craft), or found (artifact searches). Rebalanced economy at 40% baseline yield for balanced progression.
- **Trading System**: Facilitates secure trading of chi, rebirths, and artifacts between users.
- **Permanent Chest System**: Personal storage that persists across all resets and republishes, for valuable items, artifacts, potions, weapons, armor, ores, and garden seeds.
- **Event Logging System**: Comprehensive logging of bot activities to a dedicated channel using rich, color-coded embeds.
- **Developer Portal (`P!log`)**: Provides comprehensive error logging and system monitoring with pagination, command filtering, and real-time auto-posting to a configurable channel. Logs persist for 7 days.
- **Rift Event System**: A complete boss battle event (`The Rifter`) with exclusive rewards (Rift Shards for rebirths or a 4th garden tier unlock - Rift Garden). Participants are auto-equipped for combat.
- **P!setup Command**: Auto-creates all required infrastructure for new servers including Positive Chi, Negative Chi, and Quest Completer roles with proper colors, plus a panda-bot-logs event channel with correct permissions. Makes bot setup instant and foolproof.
- **Automated Systems**: Daily evaluations for role assignment and leaderboards, monthly quest resets, and milestone tracking.
- **Translation Command**: Supports direct text and message ID translation with retry logic and smart language matching.
- **Combat System**: Features 10 legendary weapons, 7 new healing items, and a comprehensive potion crafting system.
- **HP Upgrade System**: Dynamic HP calculation based on base HP, stackable artifact bonuses, and permanent HP upgrades purchasable from the Rebirth Shop.
- **Achievements System**: Gamified progression tracking with 27 achievements across 6 categories (Combat, Exploration, Collection, Social, Economy, Mastery). Features 4 tier levels (common, rare, epic, legendary), automatic unlock tracking, DM notifications with rich embeds, chi rewards (100-2500), and progress tracking via `P!achievements` command. Integrated into major milestones: first duel win, Dragon pet acquisition, and Tier 3 garden upgrade (eternal tier).

### System Design Choices
- **Asynchronous Operations**: Leverages `discord.py` and `FastAPI` with an async-safe service layer.
- **Command Prefix Handling**: Uses static prefixes `["P!", "Q!"]`.
- **Permission System**: Relies on Discord's native administrator permissions.
- **Data Persistence**: Uses a PostgreSQL database (Replit's Neon database) as the primary storage, with in-memory data synced to the database every minute. JSON files serve as backup only.
- **Multi-Server Architecture**: The database layer is refactored for guild-isolated deployment, ensuring data separation across multiple Discord servers. This includes mandatory `guild_id` parameters for all database methods, composite unique constraints, and optimized performance indexes.

## External Dependencies

### Python (Backend & Bot)
- **discord.py**: Discord API wrapper.
- **FastAPI**: Web framework.
- **uvicorn**: ASGI server.
- **pydantic**: Data validation.
- **websockets**: For real-time communication.
- **googletrans**: Free translation API.

### Node.js (Frontend)
- **React**: UI library.
- **Vite**: Build tool and dev server.

### Discord API
- Utilizes specific intents (Server Members, Message Content) and permissions (Read Messages, Send Messages, Add Reactions, Manage Roles, Read Message History).