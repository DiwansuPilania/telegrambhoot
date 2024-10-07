# telegrambhoot

import telebot
from telebot.types import ReplyKeyboardMarkup, KeyboardButton


# Replace 'YOUR_BOT_API_TOKEN' with the actual API token from BotFather
bot = telebot.TeleBot('7511809136:AAEBxjVygvDhgqe7Iq6vRWlIXkwv-tzBLtg')

# Dictionary to store user data
user_data = {}

# Function to create house selection buttons with colors represented by emojis
def create_house_buttons():
    markup = ReplyKeyboardMarkup(row_width=2)
    houses = [
        "🔵 Samrat Ashoka",          # Blue
        "🟤 Raja Krishnadevaraya",   # Maroon
        "🟢 Maharana Pratap",        # Green
        "🟠 Chhatrapati Shivaji Maharaj"  # Orange
    ]
    for house in houses:
        markup.add(KeyboardButton(house))
    return markup

# Function to create representative type buttons with emojis
def create_rep_type_buttons():
    markup = ReplyKeyboardMarkup(row_width=2)
    rep_types = ["👨‍🏫 Faculties", "👨‍🎓 Students"]
    for rep_type in rep_types:
        markup.add(KeyboardButton(rep_type))
    return markup

# Function to create faculty role buttons with emojis
def create_faculty_role_buttons():
    markup = ReplyKeyboardMarkup(row_width=2)
    roles = ["👔 Faculty In-charge", "👥 Faculty Representative"]
    for role in roles:
        markup.add(KeyboardButton(role))
    return markup

# Function to create student role buttons with emojis
def create_student_role_buttons():
    markup = ReplyKeyboardMarkup(row_width=2)
    roles = ["💼 House BE Mentor", "🏅 House Captain", "🎖 House Vice-Captain"]
    for role in roles:
        markup.add(KeyboardButton(role))
    return markup

# Function to create a restart button with emoji
def create_restart_button():
    markup = ReplyKeyboardMarkup(row_width=1)
    markup.add(KeyboardButton("🔄 Restart"))
    return markup

# Start command handler
@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.reply_to(message, "𝐀𝐚 𝐆𝐚𝐲𝐚 𝐒𝐡𝐞𝐫,𝐍𝐚𝐚𝐦 𝐏𝐮𝐜𝐡𝐧𝐞😂", reply_markup=create_house_buttons())
    # Initialize user data for this chat
    user_data[message.chat.id] = {'step': 'house_selection'}

# House selection handler
@bot.message_handler(func=lambda message: user_data.get(message.chat.id, {}).get('step') == 'house_selection')
def house_selection(message):
    houses = [
        "🔵 Samrat Ashoka",         
        "🟤 Raja Krishnadevaraya",  
        "🟢 Maharana Pratap",       
        "🟠 Chhatrapati Shivaji Maharaj"
    ]
    if message.text in houses:
        user_data[message.chat.id]['house'] = message.text
        bot.reply_to(message, "𝐀𝐛 𝐈𝐬𝐦𝐞 𝐊𝐢𝐬𝐤𝐚 𝐍𝐚𝐚𝐦 𝐁𝐡𝐮𝐥 𝐆𝐚𝐲𝐚 ", reply_markup=create_rep_type_buttons())
        user_data[message.chat.id]['step'] = 'representative_type'
    else:
        bot.reply_to(message, "𝐓𝐞𝐣 𝐍𝐚 𝐁𝐚𝐧𝐧𝐞")

# Representative type selection handler
@bot.message_handler(func=lambda message: user_data.get(message.chat.id, {}).get('step') == 'representative_type')
def representative_type_selection(message):
    if message.text == "👨‍🏫 Faculties":
        user_data[message.chat.id]['rep_type'] = message.text
        bot.reply_to(message, "𝐈𝐬𝐦𝐞 𝐊𝐨𝐧 𝐡", reply_markup=create_faculty_role_buttons())
        user_data[message.chat.id]['step'] = 'representative_role'
    elif message.text == "👨‍🎓 Students":
        user_data[message.chat.id]['rep_type'] = message.text
        bot.reply_to(message , "𝐈𝐬𝐦𝐞 𝐊𝐨𝐧 𝐡", reply_markup=create_student_role_buttons())
        user_data[message.chat.id]['step'] = 'representative_role'
    else:
        bot.reply_to(message, "𝐓𝐞𝐣 𝐍𝐚 𝐁𝐚𝐧𝐧𝐞")

# Function to retrieve contact information and associated photo
def get_contact_details_and_photo(house, rep_type, role):
    contact_data = {
        "🔵 Samrat Ashoka": {
            "👔 Faculty In-charge": ("Prof JB Jawale- 7457924466",),
            "👥 Faculty Representative": ("Dr. Dipika Birari, Mr. Anup Kadam, Ms. Gouri Bhasale, Pravin Sangle",),
            "💼 House BE Mentor": ("Ayush Ojha- 6264389700, Akriti Singh- 7457924466",),
            "🏅 House Captain": ("Ankit Yadav(ENTC)- 7494924041, Tanisha Sharma(ENTC)- 9419604895", "csmcap.jpg"),
            "🎖 House Vice-Captain": ("Akash Singh- 9571265207, Sunandha Reddy(IT)- 9571067672", "ashokavc.jpg")
        },
        "🟤 Raja Krishnadevaraya": {
            "👔 Faculty In-charge": ("Dr. Pritee Purohit- 9351447398",),
            "👥 Faculty Representative": ("Mr. Sukumar Chaughule, Mr. Yuvraj Gholap", ),
            "💼 House BE Mentor": ("Shivram- 9351447398, Ritika- 8983829429",),
            "🏅 House Captain": ("Rohit Kumar(ENTC)- 9462007939, Shaikh Haseena- 8459258517", "raja.jpg"),
            "🎖 House Vice-Captain": ("Piyush Saini- 9599478220, Kritika- 6267007012", "rkdvc.jpg")
        },
        "🟢 Maharana Pratap": {
            "👔 Faculty In-charge": ("Dr. Ashwini Sapkal- 7518470604",),
            "👥 Faculty Representative": ("Mr. Girish Kapse, Ms. Sushma Shirke, Mr. Anand", ),
            "💼 House BE Mentor": ("Pranay Puniya- 7851847604, Aditi More- 9501501733",),
            "🏅 House Captain": ("Krishan Kumar- 8941989000, Ashritha Reddy- 7386705828", "krishnacp.jpg"),
            "🎖 House Vice-Captain": ("Shivam Sharma- 8354099643, Ritika Kumari- 882469 3065", "maharana.jpg")
        },
        "🟠 Chhatrapati Shivaji Maharaj": {
            "👔 Faculty In-charge": ("Prof MB Lonare- 9971018972", "fac.jpg"),
            "👥 Faculty Representative": ("Mr. Vijay karra, Mr. Sandeep Sampleti , Dr. SM Gaikwad, Prakash K"),
            "💼 House BE Mentor": ("Piyush - 7905061506, Anushna Panwar- 9971081972",),
            "🏅 House Captain": ("Pratham Kumar- 703771998,Khushia-7850005774", "csm.jpg"),
            "🎖 House Vice-Captain": ("Shivang Kumar- 6395926392,Khushboo- 9341692964", "csmvc.jpg")
        }
    }

    if rep_type == "👨‍🏫 Faculties":
        return contact_data.get(house, {}).get(role, ("No contact information available.", None))
    elif rep_type == "👨‍🎓 Students":
        return contact_data.get(house, {}).get(role, ("No contact information available.", None))

# Representative role selection handler
@bot.message_handler(func=lambda message: user_data.get(message.chat.id, {}).get('step') == 'representative_role')
def representative_role_selection(message):
    if message.text in ["👔 Faculty In-charge", "👥 Faculty Representative", "💼 House BE Mentor", "🏅 House Captain", "🎖 House Vice-Captain"]:
        user_data[message.chat.id]['role'] = message.text
        contact_info, photo_path = get_contact_details_and_photo(user_data[message.chat.id]['house'], user_data[message.chat.id]['rep_type'], user_data[message.chat.id]['role'])

        # Send the contact info
        bot.reply_to(message, contact_info)

        # Send the photo if available
        if photo_path:
            with open(photo_path, 'rb') as photo:
                bot.send_photo(message.chat.id, photo)

        bot.reply_to(message, "Choose an option to continue:", reply_markup=create_restart_button())
        user_data[message.chat.id]['step'] = 'restart'
    else:
        bot.reply_to(message, "𝐓𝐞𝐣 𝐍𝐚 𝐁𝐚𝐧𝐧𝐞")

# Restart handler
@bot.message_handler(func=lambda message: user_data.get(message.chat.id, {}).get('step') == 'restart')
def restart(message):
    if message.text == "🔄 Restart":
        user_data[message.chat.id] = {'step': 'house_selection'}
        bot.reply_to(message, "𝐀𝐚 𝐆𝐚𝐲𝐚 𝐒𝐡𝐞𝐫, 𝐀𝐚𝐣 𝐊𝐢𝐬𝐤𝐚 𝐍𝐚𝐚𝐦 𝐁𝐡𝐮𝐥 𝐆𝐚𝐲𝐚", reply_markup=create_house_buttons())
    else:
        bot.reply_to(message, "𝐓𝐞𝐣 𝐍𝐚 𝐁𝐚𝐧𝐧𝐞")

# Start the bot
bot.polling()
