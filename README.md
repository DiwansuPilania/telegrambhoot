# telegrambhoot

House Representative Bot
This is a Telegram bot that allows users to select a house and role (Faculty or Student), and then retrieves and displays contact information along with relevant images for selected House Captains, Vice-Captains, or other roles.

Features
House Selection: Users can select from four houses:
🔵 Samrat Ashoka
🟤 Raja Krishnadevaraya
🟢 Maharana Pratap
🟠 Chhatrapati Shivaji Maharaj
Representative Type Selection: Users choose whether they are Faculty or Student.
Role Selection: Depending on the representative type, users select from roles such as:
Faculty In-charge
Faculty Representative
House BE Mentor
House Captain
House Vice-Captain
Contact Information: The bot provides contact information for the selected role.
Image Display: For certain roles like House Captain, the bot also displays an image along with the contact details.
Requirements
Python 3.7+
Dependencies: Install the required dependencies using pip:
bash
Copy code
pip install pyTelegramBotAPI
Setup
Clone the repository:

bash
Copy code
git clone https://github.com/yourusername/house-representative-bot.git
Install dependencies: Install the telebot library using pip:

bash
Copy code
pip install pyTelegramBotAPI
Get the API Token:

Create a new bot via BotFather on Telegram.
Copy the generated API token and update the bot's configuration in the code.
Add your API token: In the main.py file, replace 'YOUR_BOT_API_TOKEN' with your actual token from BotFather:

python
Copy code
bot = telebot.TeleBot('YOUR_BOT_API_TOKEN')
Prepare Images: Ensure the images for the House Captains, Vice-Captains, or Faculty are in the project directory and correctly named (e.g., csm.jpg, ashokavc.jpg, etc.).

Run the bot: Start the bot by running the following command:

bash
Copy code
python main.py
How to Use
Start the bot: Open the bot in Telegram and type /start to begin interacting.
Select a House: Choose from one of the four houses.
Select Representative Type: Choose between Faculties or Students.
Select a Role: Depending on the previous selection, choose a role such as House Captain or Faculty In-charge.
Receive Contact Information: The bot will display the contact information for the selected house and role. If available, it will also send an image.
Folder Structure
bash
Copy code
house-representative-bot/
│
├── main.py                # The main bot script
├── csm.jpg                # Image for Chhatrapati Shivaji Maharaj Captain
├── ashokavc.jpg           # Image for Samrat Ashoka Vice-Captain
├── raja.jpg               # Image for Raja Krishnadevaraya Captain
├── README.md              # This README file
└── ...                    # Other necessary images
Example Interaction
makefile
Copy code
User: /start
Bot: 𝐀𝐚 𝐆𝐚𝐲𝐚 𝐒𝐡𝐞𝐫,𝐍𝐚𝐚𝐦 𝐏𝐮𝐜𝐡𝐧𝐞😂
[House buttons appear]

User selects "🔵 Samrat Ashoka"
Bot: 𝐀𝐛 𝐈𝐬𝐦𝐞 𝐊𝐢𝐬𝐤𝐚 𝐍𝐚𝐚𝐦 𝐁𝐡𝐮𝐥 𝐆𝐚𝐲𝐚
[Representative type buttons appear]

User selects "👨‍🎓 Students"
Bot: 𝐈𝐬𝐦𝐞 𝐊𝐨𝐧 𝐡
[Role buttons appear]

User selects "🏅 House Captain"
Bot: Ankit Yadav(ENTC)- 7494924041, Tanisha Sharma(ENTC)- 9419604895
[Image of House Captain appears]
