# speechrecognitionAI
In this project I have have written code for the speech recognition.
The code is written in python.
Here is the code:

import speech_recognition as sr
import pyttsx3
import datetime

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice',voices[1].id)

def talk(text):
    engine.say(text)
    engine.runAndWait()

global command

def take_command():
    
    try:
        with sr.Microphone() as source:
            print("listening......")
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'alexa' in command:
                command = command.replace('alexa','')
                print(command)
                
    except:
        pass
    return command

def run_alexa():
    command = take_command()
    print(command)
    if 'time' in command:
        time = datetime.datetime.now().strftime('%H:%M %p')
        print(time)
        talk('The current time is ' + time)
    elif 'how are you' in command :
        print('I am fine Thank you!')
        talk('I am fine Thank you!')
    elif 'what are you feeling' in command:
        print('I am feeling good! how may i assist you.')
        talk('I am feeling good! how may i assist you.')
    
run_alexa()

