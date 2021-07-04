# Personal-Desktop-Assistant-with-Python
Desktop Personal  Assistant with Python
import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import os
import webbrowser

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
#print(voices[1].id)
engine.setProperty('voice', voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    hour = int(datetime.datetime.now().hour)
    if (hour>=0) and (hour<=12):
       speak("Good Morning")

    elif (hour>=12) and (hour<18):
       speak("Good Afternoon")

    else:
       speak("Good Evening")

    speak("I am Jarvis Ma'am. Please tell me how may i help you")





def takeCommand():   #it takes microphone input from the user and return string output

    r = sr.Recognizer()
    with sr.Microphone() as source:
        
        print("Listening...")
        r.pause_threshold = 1   #second of non speaking audio  before phrase is considered complete
        audio = r.listen(source)

    try:
        print("Recognising...")
        query = r.recognize_google(audio, language='en-in')
        print(f"user said: {query}\n")

    except Exception as e:
        print(e)
        print("say that again please....")
        return "none"

    return query
def sendEmail(to, content):
    server = smtplib.SMTP('smntp.gmail.com')

if __name__ == "__main__":
     clear = lambda: os.system('cls')
     #this function will clean any
     #command before execution of this file
     clear()
     wishMe()
     #while True:
     if 1:  # if you want to open while then comment if
        query = takeCommand().lower()
        #logic for executing task based on query
        if 'wikipedia' in query:
            speak("Searching wikipedia....")
            query = query.replace("wikipedia", " ")
            results = wikipedia.summary(query, sentences = 2)
            speak("According to wikipedia")
            print(results)
            speak(results)

        elif 'open youtube' in query:
            speak("Now you are going to youtube\n")
            webbrowser.open("youtube.com")

        elif 'open google' in query:
            speak("Now you can google anything\n")
            webbrowser.open("google.com")

        elif 'open stackoverflow' in query:
            speak("Now you are going to stackoverflow\n")
            webbrowser.open("stackoverflow.com")
        
        elif 'open internshala' in query:
            speak("Now you are going to Internshala. Enjoy courses")
            webbrowser.open("internshala.com")

        elif 'play music' in query:
            speak("now enjoy your song!!")
            webbrowser.open("https://www.youtube.com/watch?v=ZxICgeTR4SQ")
         
        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f" the time is {strTime}")

        elif 'open visual code' in query:
            speak("now you can start your code")
            codePath = "C:\\Users\\soura\\AppData\\Local\\Programs\\Microsoft VS Code"
            os.startfile(codePath)

        elif 'play song' in query:
            speak("play song....")
            musicPath = "C:\\Users\\soura\\Music\\nainowale_ne_full_video_song_padmaavat_deepika_padukone_shahid_kapoor_ranveer_singh_mp3_17873.mp3"
            os.startfile(musicPath)

        elif 'email to prachi' in query:
            try:
                speak("what should i say")
                content = takeCommand()
                to = "prachisaxena1618@gmail.com"
                sendEmail(to, content)
                speak("Email has sent")
            except Exception as e:
                print(e)
                speak("sorry my friend i am not able to send")

