# Strava Club Weekly Leaderboard Bot

[![https://i.imgur.com/U4Yvb6kl.jpg](https://i.imgur.com/U4Yvb6kl.jpg)](https://github.com/DmitryTeplov182/strava-club-leatherboard-bot)  

This Python script scrapes data from the Strava club leaderboard, providing information about the leaders of the previous week. The data is sent to users via a Telegram bot, supporting both [inline](https://core.telegram.org/api/bots/inline) and classic modes. Code uses Strava cookies to scrape data. So you need to get Strava cookies manually.  

## Features

- 🚴 **Cycling Clubs**: Shows distance, elevation gain, longest ride, and speed (km/h)
- 🏃‍♂️🏃‍♀️ **Running Clubs**: Shows distance, elevation gain, longest run, and pace (min/km)
- 🏆 **Top 5 Rankings**: Displays top 5 club members for each metric
- ⏰ **Scheduled Posts**: Automatic weekly leaderboard posts
- 📱 **Inline Mode**: Quick access to leaderboard via inline queries
- 🖼️ **Image Support**: Optional image with leaderboard text
- 💾 **Caching**: 7-day cache to reduce API calls

**DO NOT USE YOUR MAIN STRAVA ACCOUNT HERE. STRAVA CAN BAN YOU FOR SCRAPPING ANY TIME**

~~Strava is constantly struggling with data parsing. Since November 6, 2024, it's been necessary to use a [undetected_chromedriver](https://github.com/ultrafunkamsterdam/undetected-chromedriver/) and Chrome inside the container with the bot. Also, a VNC server has been added to the container. If you need to use it, uncomment the lines in the docker-compose file. The password is inside the Dockerfile.~~

I've stopped fighting with Strava's bot detection. Right now, you need to obtain cookies manually. It seems that one fresh set of cookies lasts for more than two months. If you have any ideas on how to get cookies automatically, feel free to contribute.

## Installation

### Docker Installation (Recommended)

1. **Install Docker and Docker Compose:**  
Follow the official Docker documentation to install Docker and Docker Compose on your system.
* [Docker Installation Guide](https://docs.docker.com/engine/install/)
* [Docker Compose Installation Guide](https://docs.docker.com/compose/install/)

2. **Download the necessary files:**  
Use `wget` to download the `compose.yaml` and `.env.example` files from the repository.
    ```bash
    wget https://raw.githubusercontent.com/DmitryTeplov182/strava-club-leatherboard-bot/main/compose.yaml
    wget https://raw.githubusercontent.com/DmitryTeplov182/strava-club-leatherboard-bot/main/.env.example -O .env
    ```

3. **Fill in the .env file with your data:**  
Open the `.env` file in a text editor and fill in the required information.

4. **Start the Docker services:**  
   Run the following command to start the Docker services in detached mode.  
    ```bash
       docker compose up -d
    ```

### Local Installation

1. **Clone the repository:**
    ```bash
    git clone https://github.com/DmitryTeplov182/strava-club-leatherboard-bot.git
    cd strava-club-leatherboard-bot
    ```

2. **Create virtual environment:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4. **Create and configure .env file:**
    ```bash
    cp .env.example .env
    # Edit .env with your configuration
    ```

5. **Run the bot:**
    ```bash
    python tg.py
    ```

## Configuration

Create a `.env` file with the following variables:

```env
# Bot Configuration
BOT_TOKEN=your_telegram_bot_token
GROUP_ID=your_telegram_group_id
CLUB_ID=your_strava_club_id
CLUB_TYPE=CYCLING  # or RUNNING

# Strava Configuration
STRAVA_COOKIES=[{"name":"cookie1","value":"value1"}]

# Scheduling (Optional)
SCHEDULE=false
WEEKDAY=mon
SEND_TIME=09:00

# Image (Optional)
IMAGE=false
IMAGE_URL=https://example.com/image.jpg
```

### Club Types

- **CYCLING** (default): Shows speed in km/h, cycling icons 🚴
- **RUNNING**: Shows pace in min/km, running icons 🏃‍♂️🏃‍♀️

## Usage

### Telegram Commands

- `/start` or `/help` - Show welcome message and instructions
- `/weektop` - Get current week's top 5 club members

### Inline Mode

Type `@your_bot_name` in any chat and select "Top 5 Club Members" to quickly get the leaderboard.

## Disclaimer

**DO NOT USE YOUR MAIN STRAVA ACCOUNT HERE. STRAVA CAN BAN YOU FOR SCRAPING ANY TIME**  
The author assumes no responsibility for any errors or omissions in the content of this code. The information contained in this code is provided on an "as is" basis with no guarantees of completeness, accuracy, usefulness, or timeliness. The author shall not be liable for any losses, injuries, or damages from the use of this code.

## License  
This project is licensed under the Beerware license. As long as you retain this notice, you can do whatever you want with this stuff. If we meet someday, and you think this stuff is worth it, you can buy me a beer in return.

---

🤖 **AI-Powered Development**  
This project was developed with the assistance of AI tools, demonstrating how modern AI can enhance software development workflows and help create more robust and feature-rich applications.
