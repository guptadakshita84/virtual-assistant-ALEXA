# virtual-assistant-ALEXA
       


import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
import pyjokes
import pyaudio

listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)


def talk(text):
    print(text)
    engine.say(text)
    engine.runAndWait()


def take_command():
        with sr.Microphone() as source:
            voice = listener.adjust_for_ambient_noise(source)
            print('listening...')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'alexa' in command:
                command = command.replace('alexa', '')
        return command


def run_alexa():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
    elif 'who the heck is' in command:
        person = command.replace('who the heck is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'date' in command:
        talk("it is eighth of September")
    elif 'are you single' in command:
        talk('I am in a relationship with wifi')
    elif 'hello' in command:
        talk('hey ya , whats up')
    elif 'i love you' in command:
        talk('I love you too')
    elif 'you are beautiful lady' in command:
        talk('thank you so much and you are cute as hell')
    elif 'thanks' in command:
        talk('pleasure')
    elif 'joke' in command:
        talk(pyjokes.get_joke())
    else:
        talk('Please say the command again.')


while True:
    run_alexa()
