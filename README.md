# 🍰 20 Questions: The Case of Grandad's Missing Cake

<div align="center">

**A mobile detective game powered by AI where you interrogate suspects to solve the mystery!**

*Who ate Grandad's cake? You have 20 questions to find out...*

</div>

## 🎮 About The Game

Grandad's delicious cake has been eaten, and all that remains are crumbs! As the detective on the case, you must interrogate Grandad's two grandchildren - Charlotte and Gary - to determine who the culprit is. But there's a catch: **you only have 20 questions!**

This isn't your typical point-and-click adventure. Each conversation is unique because the NPCs are powered by AI through the Anthropic Claude API. Charlotte and Gary will respond naturally to your questions, remember what you've asked, and react based on their guilt (or innocence). Every playthrough is different!


## 🎨 Screenshots

<div align="center">

<img src="screenshots/screenshot1.png" width="300" alt="Main Menu"> <img src="screenshots/screenshot2.png" width="300" alt="Gameplay">

*Gameplay*

<img src="screenshots/screenshot3.png" width="300" alt="Conversation"> <img src="screenshots/screenshot4.png" width="300" alt="Making a Guess">

*Interrogation*

</div>


## ✨ Features

- 🎨 **Top-down 2D exploration** - Navigate a charming pixel art world with virtual joystick controls
- 🤖 **AI-Powered NPCs** - Have real conversations with suspects powered by Claude AI
- 🕵️ **Limited Questions** - Only 20 questions to solve the case - choose wisely!
- 📱 **Mobile-First Design** - Optimized for mobile gameplay with touch controls
- 🗺️ **Custom Tilemap** - Explore a hand-crafted outdoor environment
- 💬 **Dynamic Dialogue** - Every conversation is unique based on your questions
- 🎯 **Make Your Accusation** - When you think you know who did it, make your guess!

## 🎯 How to Play

1. **Explore** the map using the virtual joystick
2. **Approach** Charlotte or Gary to start a conversation
3. **Ask Questions** to gather clues (you have 20 total!)
4. **Analyze** their responses - are they hiding something?
5. **Make Your Guess** by clicking the exclamation mark icon when ready
6. **Solve the Mystery** - Did you catch the cake thief?

## 🛠️ Tech Stack

- **Game Engine**: Phaser 3 (v3.55.2)
- **AI Backend**: Anthropic Claude API (via Cloudflare Workers)
- **Controls**: Rex Virtual Joystick Plugin
- **Map Design**: Tiled Map Editor
- **Frontend**: Vanilla JavaScript, HTML5, CSS3

## 📋 Requirements

### API Setup

This game requires access to the **Anthropic Claude API**. The API calls are routed through a Cloudflare Worker for secure key management.

**You'll need:**
1. An Anthropic API (or chosen LLM) key 
2. A Cloudflare Workers account (free tier works!)
3. The Cloudflare Worker deployed at: `https://api-call.youruserhere.workers.dev/`

### Cloudflare Worker Configuration

The worker handles two endpoints:

- `POST /` - Processes player questions and returns AI-generated NPC responses
- `POST /guess` - Validates the player's final accusation

**Expected request format:**
```javascript
// For questions
{
  "input": "Did you eat the cake?",
  "npc": "charlotte" or "gary",
  "sessionId": "unique-session-id"
}

// For guesses
{
  "npc": "charlotte" or "gary",
  "sessionId": "unique-session-id"
}
```

### Environment Setup

Your Cloudflare Worker needs to be configured with:
- Anthropic API key stored as an environment variable
- Session management to maintain conversation context
- CORS headers enabled for web requests

## 🚀 Getting Started

### Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/20-questions-game.git
cd 20-questions-game
```

2. Set up your Cloudflare Worker:
   - Create a new Cloudflare Worker
   - Add your Anthropic API key to the worker's environment variables
   - Deploy the worker and update the API endpoint in `script.js`

3. Serve the game locally:
```bash
# Using Python
python -m http.server 8000

# Or using Node.js
npx http-server
```

4. Open your browser and navigate to `http://localhost:8000`

### File Structure

```
├── index.html              # Main menu
├── game.html              # Game interface
├── script.js              # Game logic and AI integration
├── style.css              # Styling
├── sprites/               # Character and UI sprites
│   ├── player1sprite.png
│   ├── girl1sprite.png
│   ├── guy1sprite.png
│   ├── girl1.png
│   ├── guy1.png
│   ├── grandad.png
│   ├── homeicon.png
│   └── exclamationmarkicon.png
└── tileset/               # Map tiles and data
    ├── outside1.png
    ├── outside2.png
    ├── outside3.png
    ├── outsidemap.json
    └── outsidemap.tmx
```

## 🎲 Game Mechanics

### Question Counter
- Displayed at the top of the screen
- Increments with each question asked to either NPC
- When you reach 20 questions, you must make your accusation

### Early Guessing
- Click the ❗ icon (appears after 2 questions) to make an early guess
- Can you solve the case before running out of questions?

### Session Management
- Each playthrough generates a unique session ID
- Conversations are maintained throughout the session
- NPCs remember what you've discussed

### AI Behavior
- Charlotte and Gary have consistent personalities
- One is guilty, one is innocent (randomized each session)
- They respond naturally to your questions with context awareness

## 🔧 Configuration

### Customizing the AI Behavior

To modify how the NPCs behave, you'll need to update the system prompts in your Cloudflare Worker. You can adjust:
- Personality traits
- Response styles
- Guilt indicators
- Backstory details

### Adjusting Game Difficulty

Edit `script.js` to change:
- Maximum number of questions (line 495: `if (parseInt(questionCounter) >= 20)`)
- NPC movement speed (line 406: `randomSpeed()` function)
- Question counter reveal threshold (line 524: early guess availability)

## 🤝 Contributing

Contributions are welcome! Here are some ideas for improvements:

- [ ] Add more NPCs and suspects
- [ ] Multiple mystery scenarios
- [ ] Hint system
- [ ] Difficulty levels
- [ ] Score tracking
- [ ] Sound effects and music
- [ ] Additional maps and locations
- [ ] Clue collection system

## 📝 License

This project is open source and available under the MIT License.

## 🙏 Acknowledgments

- **Phaser** - Amazing game framework
- **Anthropic Claude** - AI-powered conversations
- **Rex Virtual Joystick** - Mobile controls plugin
- **Tiled Map Editor** - Level design tool
- Pixel art sprites and tilesets (credit original creators if using third-party assets)

## 🐛 Known Issues

- Camera occasionally needs manual reset after conversations
- Session persistence requires localStorage support
- Mobile keyboard can sometimes obscure input field

## 💡 Tips for Players

1. **Start broad** - Ask general questions before getting specific
2. **Watch for contradictions** - NPCs might slip up!
3. **Note their reactions** - The AI generates contextual responses
4. **Don't waste questions** - Think before you ask
5. **Trust your instincts** - Sometimes the answer is in what they DON'T say

---

<div align="center">

**Ready to solve the mystery?**

🍰 *Good luck, Detective!* 🔍

</div>
