# FeurBotte
bot tweeter qui a pour objectif de répondre feur au mesage ce terminant par quoi.

# Code
import tweepy

auth = tweepy.OAuthHandler("consumer_key","consumer_secret")
auth.set_access_token('acces_token','acces_token_secret')

api = tweepy.API(auth)

try:
    api.verify_credentials()
    print("Le bot est prêt pour la blague")
except:
    print("erreur de connexion")

max_tweets = 200000
tweets = tweepy.Cursor(api.search_tweets, q='quoi').items(max_tweets)
key = ['quoi']

for tweet in tweets:
    text = str(tweet.text).split(' ')
    last_word = text[-1]
    if str(last_word) == key[0]:
        api.update_status('feur', in_reply_to_status_id=tweet.id_str, auto_populate_reply_metadata=True)
        print(tweet.text + ' | feur')
    else:
        pass
