

# Financial Analyst Chatbot
I am writing this README in a very informal manner by hand (no gpt) so its actually interesting to read :).....so I would really appreciate it if you go through it.
## How to use it?

### Folder structure...
So before I tell you about what the project is about? How it works? I would first like you to experience it. The "notebooks" folder contains several .ipynb notebooks which I created during the learning process, each one of them actually contains an essential part of the final project, they can be read to review my learning path. The folder also contains many(6) **prototypes** which are essentially different versions of my project, all with different features. Prototypes 1 to 4 require mounting my google drive so you can't run them but prototype 5 and 6 can be run just by clicking "run all" on colab.

### Prototype 6 (The final one)

In the notebooks folder of Task2+Task3 there is **Prototype6(Final)**. I would like you to download it, upload it on colab and hit run all, it will take around 3 mins to cold-start (install libraries, define function etc etc) and in the last cell you will find a gradio link which will lead you to the web app for the chatbot. You can ask it to explain trends in stock prices of virtually any ticker (but more reliable for famous ones like apple, microsoft, nvidia etc). You can do this for any timeline by saying "for today, last year, last month, yesterday etc etc" or just specify the date in prompt. You can just input the organization's name or ticker or both, just make sure its recognizable, for example write Explain stocks of **Apple Inc** instead of just apple or **nvidia corp** instead of nvidia (Microsoft, American Airlines etc etc work fine). And the chatbot takes around 40secs to answer each query so don't worry, its gonna answer :)

Some prompts that work for sure-

 - Explain me the trends in stock prices of apple inc last month
 - Explain me the trends in stock prices of microsoft last month (or last year or anything timeline)
 - Compare the stock prices of apple inc and nvidia corp and tell me if they are somehow correlated. 

But you can always try your own prompts,
If somethings working, there can only be two reasons.

 1. It can't detect the name of organization, try to include it in a more formal way as discussed earlier
 2. Or the alpha vantage api key has expired(or has been overused, kindly update it in cell **5**
## How it works? 
I am just explaining the workflow, the code is explain through comments in the notebook. All the code is from documentations and I have added my own logic on top of it, there is very minimal vibecoding (it doesn't work anyways) in this project.
 1. The user enters the prompt in the webapp
 2. It is given to the function parse_question which uses nlp to extract, timelines, organisations from the question. Any time detected is converted to datetime objects. Also using basic regex to detect if user has directly provided the ticker like AAPL.
 3. The organizations detected are converted into their respective symbols by matching it from a dataset which I wget from my drive
 4. News for it gets fetched using alphavantage (time specific news) and its filtered based on the sentiment score provided by alphavantage.
 5. Use trafilatura to read the webpages alphavantage provided for more info
 6. Doc objects are built out of everything gathered and its split into chunks.
 7. Vector(FAISS) database of the chunks is prepared where I include the ticker name, time etc manually for more accurate search results later.
 8. Financial numbers are fetched from yfinance and added to the text provided by the similarity search so that news can be correlated to actual numbers.
 9. A graph is also plotted based on closing prices provided by yfinance (if u say last month in prompt,only one months graph will be plotted, so its time aware)
 10. This all take around 40secs and gets displayed on gradio webapp after its done :))

It was all working when I checked lasttime, but if its not please contact me asap :-)

