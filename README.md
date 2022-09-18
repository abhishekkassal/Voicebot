# Voicebot
#Python program that responds the user commands


import speech_recognition as sr
import pyttsx3
import os
speech = sr.Recognizer()

try:
    engine = pyttsx3.init()
except ImportError:
        print('Requested driver not found')
except RuntimeError:
    print('Driver fails to initialize')

    voices = engine.getProperty('voices')


engine.setProperty('voice','HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Speech\Voices\Tokens\TTS_MS_EN-US_DAVID_11.0')
rate=engine.getProperty('rate')
engine.setProperty('rate',rate)

def speak_text_cmd(cmd):
    engine.say(cmd)
    engine.runAndWait()

def read_voice_cmd():
    voice_text=''
    print('Listening...')
    with sr.Microphone() as source:

       audio = speech.listen(source)

    try:
       voice_text = speech.recognize_google(audio)
    except sr.UnknownValueError:
       pass
    except sr.RequestError as e:
        print('Network error.')
    return voice_text


if __name__ == '__main__':
    speak_text_cmd('this is Jazz ')

    while True:

        voice_note=read_voice_cmd()
        print('cmd:()'.format(voice_note))
        if 'test' in voice_note:
            speak_text_cmd('ok sir ')
            continue
        elif 'open' in voice_note:
            os.system('explorer C:\\{}'.format(voice_note.replace('open','')))
            continue
        elif 'sleep' in voice_note:
            speak_text_cmd('By sir')
            exit()
