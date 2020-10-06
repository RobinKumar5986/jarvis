# jarvis
'''it is an AI it recognize the voice command and also return the appropriate result it is made by python and its its name is inspired by movie IRON MAN'''
import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser as wb
import os


#import pyaudio


engine=pyttsx3.init('sapi5')
voices=engine.getProperty('voices')
#print(voices[0].id) 'mail voice id'
#print(voices[1].id) 'femail voice id'
engine.setProperty('voice',voices[0].id)

#defining speeak function
def speak(audio):
    engine.say(audio)
    engine.runAndWait()
def wishMe():
    hr=int(datetime.datetime.now().hour)
    if hr>=0 and hr<=12:
        speak('good morning')
    elif hr>=12 and hr<18:
        speak('good afternoon')
    else:
        speak('good evening!')
    speak("hello sir 'I am JARVIS' how can I help you")

#start defining intake of commands
def takecommand():
    #it takes microphone as input and return string as output
    r=sr.Recognizer()
    with sr.Microphone() as source:
        print('Listening........')
        r.pause_threshold=1
        r.energy_threshold=200
        audio=r.listen(source)
        #print(audio)
    try:
        print("Reconizing...")
        query=r.recognize_google(audio,language='en-in')
        print("user said:",query)
    except Exception as e:
        #print(e)
        print("say that again plz...")
        return'None'
    return query

if __name__=="__main__":
    wishMe()
    while True:
    #if 1:
        query=takecommand().lower()
        #logic for executing task based on query
        if 'wikipedia' in query:
            speak('searching wikipedia...')
            query=query.replace('wikipedia','')
            results=wikipedia.summary(query,sentences=2)
            speak('According to wikipedia')
            print("result")
            speak(results)
        elif 'youtube' in query:
            wb.open("https://www.youtube.com/")
        elif "google" in query:
            wb.open('https://www.google.com/')
        elif "time" in query:
            strTime=datetime.datetime.now().strftime('%H')
            strTime1=datetime.datetime.now().strftime('%M')
            strTime2=datetime.datetime.now().strftime('%S')
            speak(f'sir, the time is \t\t,{strTime}hour ,{strTime1}minuts and {strTime2} seconds ')
        elif "python" in query:
            python_path="C:\\python\\Lib\\idlelib\\idle.pyw"
            os.startfile(python_path)
        elif 'paint' in query:
            paint_path='C:\\ProgramData\\Microsoft\\Windows\\Start Menu\\Programs\\Accessories'
            os.startfile(f'{paint_path}')
        elif 'search' in query:
            print(query)
            speak('this is what i got in web')
            wb.open(f'{query}')
        
        #if "shutdown" or "shut down" in query:
         #   break
            
        
   
