
Alicia Sigmon, als333@pitt.edu, 10/06/2017

# Dialect Project: Twitter


```python
import tweepy
import pandas as pd
import matplotlib.pyplot as plt
```


```python
# Turn off pretty print# Show all output
%pprint
```

    Pretty printing has been turned OFF
    


```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```


```python
consumerKey= 'XXXXXXXXXXXXXXX'
consumerSecret='XXXXXXXXXXXXXXXX'

# Creating Authentication
auth = tweepy.OAuthHandler(consumer_key=consumerKey, 
                           consumer_secret=consumerSecret)
# Connecting to Twitter API with the authentication
api=tweepy.API(auth)
```

## #Australia


```python
# Search for '#Australia'
result = api.search(q='%23Australia')  # "%23" == "#"
len(result)
```




    13




```python
# First tweet (in json format)
tweet = result[0]

# Analyzing the first tweet on all keys in the directory (except for key names beginning with "_")
for param in dir(tweet):
    if not param.startswith("_"):
        print("%s : %s\n" % (param, eval('tweet.'+param)))
```

    author : User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none')
    
    contributors : None
    
    coordinates : None
    
    created_at : 2017-10-07 22:32:58
    
    destroy : <bound method Status.destroy of Status(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'created_at': 'Sat Oct 07 22:32:58 +0000 2017', 'id': 916793499915214848, 'id_str': '916793499915214848', 'text': 'And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', 'truncated': True, 'entities': {'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com" rel="nofollow">Twitter Web Client</a>', 'in_reply_to_status_id': None, 'in_reply_to_status_id_str': None, 'in_reply_to_user_id': None, 'in_reply_to_user_id_str': None, 'in_reply_to_screen_name': None, 'user': {'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': True, 'quoted_status_id': 916684795660394496, 'quoted_status_id_str': '916684795660394496', 'quoted_status': {'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, 'retweet_count': 0, 'favorite_count': 0, 'favorited': False, 'retweeted': False, 'possibly_sensitive': False, 'lang': 'en'}, created_at=datetime.datetime(2017, 10, 7, 22, 32, 58), id=916793499915214848, id_str='916793499915214848', text='And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', truncated=True, entities={'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, metadata={'iso_language_code': 'en', 'result_type': 'recent'}, source='Twitter Web Client', source_url='http://twitter.com', in_reply_to_status_id=None, in_reply_to_status_id_str=None, in_reply_to_user_id=None, in_reply_to_user_id_str=None, in_reply_to_screen_name=None, author=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), user=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), geo=None, coordinates=None, place=None, contributors=None, is_quote_status=True, quoted_status_id=916684795660394496, quoted_status_id_str='916684795660394496', quoted_status={'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, retweet_count=0, favorite_count=0, favorited=False, retweeted=False, possibly_sensitive=False, lang='en')>
    
    entities : {'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}
    
    favorite : <bound method Status.favorite of Status(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'created_at': 'Sat Oct 07 22:32:58 +0000 2017', 'id': 916793499915214848, 'id_str': '916793499915214848', 'text': 'And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', 'truncated': True, 'entities': {'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com" rel="nofollow">Twitter Web Client</a>', 'in_reply_to_status_id': None, 'in_reply_to_status_id_str': None, 'in_reply_to_user_id': None, 'in_reply_to_user_id_str': None, 'in_reply_to_screen_name': None, 'user': {'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': True, 'quoted_status_id': 916684795660394496, 'quoted_status_id_str': '916684795660394496', 'quoted_status': {'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, 'retweet_count': 0, 'favorite_count': 0, 'favorited': False, 'retweeted': False, 'possibly_sensitive': False, 'lang': 'en'}, created_at=datetime.datetime(2017, 10, 7, 22, 32, 58), id=916793499915214848, id_str='916793499915214848', text='And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', truncated=True, entities={'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, metadata={'iso_language_code': 'en', 'result_type': 'recent'}, source='Twitter Web Client', source_url='http://twitter.com', in_reply_to_status_id=None, in_reply_to_status_id_str=None, in_reply_to_user_id=None, in_reply_to_user_id_str=None, in_reply_to_screen_name=None, author=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), user=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), geo=None, coordinates=None, place=None, contributors=None, is_quote_status=True, quoted_status_id=916684795660394496, quoted_status_id_str='916684795660394496', quoted_status={'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, retweet_count=0, favorite_count=0, favorited=False, retweeted=False, possibly_sensitive=False, lang='en')>
    
    favorite_count : 0
    
    favorited : False
    
    geo : None
    
    id : 916793499915214848
    
    id_str : 916793499915214848
    
    in_reply_to_screen_name : None
    
    in_reply_to_status_id : None
    
    in_reply_to_status_id_str : None
    
    in_reply_to_user_id : None
    
    in_reply_to_user_id_str : None
    
    is_quote_status : True
    
    lang : en
    
    metadata : {'iso_language_code': 'en', 'result_type': 'recent'}
    
    parse : <bound method Status.parse of <class 'tweepy.models.Status'>>
    
    parse_list : <bound method Model.parse_list of <class 'tweepy.models.Status'>>
    
    place : None
    
    possibly_sensitive : False
    
    quoted_status : {'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}
    
    quoted_status_id : 916684795660394496
    
    quoted_status_id_str : 916684795660394496
    
    retweet : <bound method Status.retweet of Status(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'created_at': 'Sat Oct 07 22:32:58 +0000 2017', 'id': 916793499915214848, 'id_str': '916793499915214848', 'text': 'And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', 'truncated': True, 'entities': {'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com" rel="nofollow">Twitter Web Client</a>', 'in_reply_to_status_id': None, 'in_reply_to_status_id_str': None, 'in_reply_to_user_id': None, 'in_reply_to_user_id_str': None, 'in_reply_to_screen_name': None, 'user': {'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': True, 'quoted_status_id': 916684795660394496, 'quoted_status_id_str': '916684795660394496', 'quoted_status': {'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, 'retweet_count': 0, 'favorite_count': 0, 'favorited': False, 'retweeted': False, 'possibly_sensitive': False, 'lang': 'en'}, created_at=datetime.datetime(2017, 10, 7, 22, 32, 58), id=916793499915214848, id_str='916793499915214848', text='And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', truncated=True, entities={'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, metadata={'iso_language_code': 'en', 'result_type': 'recent'}, source='Twitter Web Client', source_url='http://twitter.com', in_reply_to_status_id=None, in_reply_to_status_id_str=None, in_reply_to_user_id=None, in_reply_to_user_id_str=None, in_reply_to_screen_name=None, author=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), user=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), geo=None, coordinates=None, place=None, contributors=None, is_quote_status=True, quoted_status_id=916684795660394496, quoted_status_id_str='916684795660394496', quoted_status={'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, retweet_count=0, favorite_count=0, favorited=False, retweeted=False, possibly_sensitive=False, lang='en')>
    
    retweet_count : 0
    
    retweeted : False
    
    retweets : <bound method Status.retweets of Status(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'created_at': 'Sat Oct 07 22:32:58 +0000 2017', 'id': 916793499915214848, 'id_str': '916793499915214848', 'text': 'And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', 'truncated': True, 'entities': {'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com" rel="nofollow">Twitter Web Client</a>', 'in_reply_to_status_id': None, 'in_reply_to_status_id_str': None, 'in_reply_to_user_id': None, 'in_reply_to_user_id_str': None, 'in_reply_to_screen_name': None, 'user': {'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': True, 'quoted_status_id': 916684795660394496, 'quoted_status_id_str': '916684795660394496', 'quoted_status': {'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, 'retweet_count': 0, 'favorite_count': 0, 'favorited': False, 'retweeted': False, 'possibly_sensitive': False, 'lang': 'en'}, created_at=datetime.datetime(2017, 10, 7, 22, 32, 58), id=916793499915214848, id_str='916793499915214848', text='And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp', truncated=True, entities={'hashtags': [{'text': 'Australia', 'indices': [7, 17]}, {'text': 'OurABC', 'indices': [19, 26]}, {'text': 'TheirABC', 'indices': [37, 46]}, {'text': 'StateBroadcaster', 'indices': [57, 74]}, {'text': 'PublicBroadcaster', 'indices': [80, 98]}], 'symbols': [], 'user_mentions': [], 'urls': [{'url': 'https://t.co/ZqMiTzVFkp', 'expanded_url': 'https://twitter.com/i/web/status/916793499915214848', 'display_url': 'twitter.com/i/web/status/9…', 'indices': [117, 140]}]}, metadata={'iso_language_code': 'en', 'result_type': 'recent'}, source='Twitter Web Client', source_url='http://twitter.com', in_reply_to_status_id=None, in_reply_to_status_id_str=None, in_reply_to_user_id=None, in_reply_to_user_id_str=None, in_reply_to_screen_name=None, author=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), user=User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none'), geo=None, coordinates=None, place=None, contributors=None, is_quote_status=True, quoted_status_id=916684795660394496, quoted_status_id_str='916684795660394496', quoted_status={'created_at': 'Sat Oct 07 15:21:01 +0000 2017', 'id': 916684795660394496, 'id_str': '916684795660394496', 'text': 'Anyway this ramble about radio &amp; Fairness Doctrine was inspired by Trump\'s call for "equal time" in late-night. As odd as that is.', 'truncated': False, 'entities': {'hashtags': [], 'symbols': [], 'user_mentions': [], 'urls': []}, 'metadata': {'iso_language_code': 'en', 'result_type': 'recent'}, 'source': '<a href="http://twitter.com/download/iphone" rel="nofollow">Twitter for iPhone</a>', 'in_reply_to_status_id': 916684147313270785, 'in_reply_to_status_id_str': '916684147313270785', 'in_reply_to_user_id': 18117833, 'in_reply_to_user_id_str': '18117833', 'in_reply_to_screen_name': 'RachelLarris', 'user': {'id': 18117833, 'id_str': '18117833', 'name': 'Rachel Joy Larris', 'screen_name': 'RachelLarris', 'location': 'Washington, DC', 'description': "World's Best Aaron Sorkin hater. I am about all things journalism, women's rights, Arlington, VA, and walking my cat on a leash.", 'url': None, 'entities': {'description': {'urls': []}}, 'protected': False, 'followers_count': 3343, 'friends_count': 2457, 'listed_count': 202, 'created_at': 'Sun Dec 14 15:49:53 +0000 2008', 'favourites_count': 4354, 'utc_offset': -14400, 'time_zone': 'Eastern Time (US & Canada)', 'geo_enabled': True, 'verified': True, 'statuses_count': 29590, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'BADFCD', 'profile_background_image_url': 'http://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_image_url_https': 'https://pbs.twimg.com/profile_background_images/378800000107546616/f52677cc5fe93d4236f0bf2af6aa06de.jpeg', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/698930331278180352/uNpImJ2G_normal.jpg', 'profile_banner_url': 'https://pbs.twimg.com/profile_banners/18117833/1402853815', 'profile_link_color': 'FF0000', 'profile_sidebar_border_color': 'FFFFFF', 'profile_sidebar_fill_color': 'FFF7CC', 'profile_text_color': '0C3E53', 'profile_use_background_image': True, 'has_extended_profile': True, 'default_profile': False, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, 'geo': None, 'coordinates': None, 'place': None, 'contributors': None, 'is_quote_status': False, 'retweet_count': 2, 'favorite_count': 5, 'favorited': False, 'retweeted': False, 'lang': 'en'}, retweet_count=0, favorite_count=0, favorited=False, retweeted=False, possibly_sensitive=False, lang='en')>
    
    source : Twitter Web Client
    
    source_url : http://twitter.com
    
    text : And in #Australia 
    #OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp
    
    truncated : True
    
    user : User(_api=<tweepy.api.API object at 0x0000023EC23140B8>, _json={'id': 2386229700, 'id_str': '2386229700', 'name': "Just Judith'n'ALF", 'screen_name': 'JrehnJ', 'location': 'Adelaide Hills, SA', 'description': "Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", 'url': 'http://t.co/s84upb1aIQ', 'entities': {'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, 'protected': False, 'followers_count': 2653, 'friends_count': 3544, 'listed_count': 254, 'created_at': 'Thu Mar 13 03:20:18 +0000 2014', 'favourites_count': 53372, 'utc_offset': None, 'time_zone': None, 'geo_enabled': True, 'verified': False, 'statuses_count': 110163, 'lang': 'en', 'contributors_enabled': False, 'is_translator': False, 'is_translation_enabled': False, 'profile_background_color': 'C0DEED', 'profile_background_image_url': 'http://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_image_url_https': 'https://abs.twimg.com/images/themes/theme1/bg.png', 'profile_background_tile': False, 'profile_image_url': 'http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_image_url_https': 'https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', 'profile_link_color': '1DA1F2', 'profile_sidebar_border_color': 'C0DEED', 'profile_sidebar_fill_color': 'DDEEF6', 'profile_text_color': '333333', 'profile_use_background_image': True, 'has_extended_profile': False, 'default_profile': True, 'default_profile_image': False, 'following': None, 'follow_request_sent': None, 'notifications': None, 'translator_type': 'none'}, id=2386229700, id_str='2386229700', name="Just Judith'n'ALF", screen_name='JrehnJ', location='Adelaide Hills, SA', description="Living through Australia's real-life replication of the Stanford Experiment. We are the guards; Asylum Seekers are the prisoners. Truly.", url='http://t.co/s84upb1aIQ', entities={'url': {'urls': [{'url': 'http://t.co/s84upb1aIQ', 'expanded_url': 'http://thispatchofremnantscrub.blogspot.com.au/2010/04/here-it-is.html', 'display_url': '…ispatchofremnantscrub.blogspot.com.au/2010/04/here-i…', 'indices': [0, 22]}]}, 'description': {'urls': []}}, protected=False, followers_count=2653, friends_count=3544, listed_count=254, created_at=datetime.datetime(2014, 3, 13, 3, 20, 18), favourites_count=53372, utc_offset=None, time_zone=None, geo_enabled=True, verified=False, statuses_count=110163, lang='en', contributors_enabled=False, is_translator=False, is_translation_enabled=False, profile_background_color='C0DEED', profile_background_image_url='http://abs.twimg.com/images/themes/theme1/bg.png', profile_background_image_url_https='https://abs.twimg.com/images/themes/theme1/bg.png', profile_background_tile=False, profile_image_url='http://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_image_url_https='https://pbs.twimg.com/profile_images/912490937808445440/1D7hU-s8_normal.jpg', profile_link_color='1DA1F2', profile_sidebar_border_color='C0DEED', profile_sidebar_fill_color='DDEEF6', profile_text_color='333333', profile_use_background_image=True, has_extended_profile=False, default_profile=True, default_profile_image=False, following=False, follow_request_sent=None, notifications=None, translator_type='none')
    
    


```python
# Individual keys
tweet.lang
tweet.text
tweet.retweet_count

# Why aren't the keys below outputting anything?
tweet.place
tweet.geo
```




    'en'






    'And in #Australia \n#OurABC  becoming #TheirABC  ... more #StateBroadcaster than #PublicBroadcaster (the news sectio… https://t.co/ZqMiTzVFkp'






    0




```python
#tweet.user
    # Looking at inidividual keys under user
tweet.user.location
tweet.user.time_zone
tweet.created_at
tweet.user.name
tweet.user.screen_name
```




    'Adelaide Hills, SA'






    datetime.datetime(2017, 10, 7, 22, 32, 58)






    "Just Judith'n'ALF"






    'JrehnJ'




```python
results = []

#Get the first 5000 items based on the search query
for tweet in tweepy.Cursor(api.search, q='%23Australia').items(2500):
    results.append(tweet)

# Verify the number of items returned
print(len(results))
```

    2500
    


```python
# Checking for duplicate Tweets
tweet_ids=[x.id for x in results]
orig_tweet_ids=set(tweet_ids)
len(tweet_ids) == len(orig_tweet_ids)
len(tweet_ids)
```




    True






    1523




```python
help(results.remove)
```

    Help on built-in function remove:
    
    remove(...) method of builtins.list instance
        L.remove(value) -> None -- remove first occurrence of value.
        Raises ValueError if the value is not present.
    
    


```python
tweet_texts=[x.text for x in results]
len(tweet_texts)==len(set(tweet_texts))
len(set(tweet_texts))

len(results) 
```




    False






    1513






    1581




```python
tweet_texts2=[]
for x in results:
    if x.text not in tweet_texts2:
        tweet_texts2.append(x.text)
    else:
        results.remove(x)
        
len(results)
```




    1523




```python
# Converts given tweet list into Pandas DataFrame, consisting of values only

def toDataFrame(tweets):
    DataSet = pd.DataFrame()
    
    DataSet['tweetID'] = [tweet.id for tweet in tweets]
    DataSet['tweetText'] = [tweet.text for tweet in tweets]
    DataSet['tweetRetweetCt'] = [tweet.retweet_count for tweet in tweets]
    DataSet['tweetSource'] = [tweet.source for tweet in tweets]
    DataSet['tweetCreated'] = [tweet.created_at for tweet in tweets]


    DataSet['userID'] = [tweet.user.id for tweet in tweets]
    DataSet['userScreen'] = [tweet.user.screen_name for tweet 
    in tweets]
    DataSet['userName'] = [tweet.user.name for tweet in tweets]
    DataSet['userCreateDt'] = [tweet.user.created_at for tweet 
    in tweets]
    DataSet['userDesc'] = [tweet.user.description for tweet in tweets]
    DataSet['userFollowerCt'] = [tweet.user.followers_count for tweet 
    in tweets]
    DataSet['userFriendsCt'] = [tweet.user.friends_count for tweet 
    in tweets]
    DataSet['userLocation'] = [tweet.user.location for tweet in tweets]
    DataSet['userTimezone'] = [tweet.user.time_zone for tweet 
    in tweets]

    return DataSet

#Pass the tweets list to 'toDataFrame' to create the DataFrame
DataSet = toDataFrame(results)
```


```python
# Verify DataFrame:
DataSet.head(10)
DataSet.tail(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>916796989186199553</td>
      <td>RT @OurNineAngelsBR: [#SUNNYSTAGRAM] 07.10.17 ...</td>
      <td>5</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:46:50</td>
      <td>909539867016785922</td>
      <td>bowonwoo</td>
      <td>weme meki</td>
      <td>2017-09-17 22:09:37</td>
      <td>My love, my beauty 💎</td>
      <td>27</td>
      <td>88</td>
      <td>Fortaleza, Brasil</td>
      <td>None</td>
    </tr>
    <tr>
      <th>1</th>
      <td>916796927378886657</td>
      <td>RT @Sassephoto: Southern Milky Way #Australia ...</td>
      <td>108</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:46:35</td>
      <td>41829156</td>
      <td>hatzbymm</td>
      <td>Margaret</td>
      <td>2009-05-22 15:07:50</td>
      <td>HATZ by Monique and Margaret are a mother and ...</td>
      <td>2161</td>
      <td>2089</td>
      <td>London</td>
      <td>London</td>
    </tr>
    <tr>
      <th>2</th>
      <td>916796911452954624</td>
      <td>RT @savillj013: #Insiders #Australia contempla...</td>
      <td>1</td>
      <td>Twitter for iPad</td>
      <td>2017-10-07 22:46:31</td>
      <td>2401117104</td>
      <td>greensinspa</td>
      <td>Betty G</td>
      <td>2014-03-21 07:07:40</td>
      <td>Nonsense Free Zone\nFeminist, Social Justice  ...</td>
      <td>2623</td>
      <td>2287</td>
      <td>Sydney Australia</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>916796902586404864</td>
      <td>Medianet news hub - aap medianet's #Brisbane, ...</td>
      <td>0</td>
      <td>Arduino</td>
      <td>2017-10-07 22:46:29</td>
      <td>4838520568</td>
      <td>Tian_A1</td>
      <td>Tian_A1 (Thierry)</td>
      <td>2016-01-23 13:06:53</td>
      <td>| The best way to predict your future is to cr...</td>
      <td>1463</td>
      <td>985</td>
      <td>Arcachon, France</td>
      <td>Paris</td>
    </tr>
    <tr>
      <th>4</th>
      <td>916796851713724416</td>
      <td>RT @Ryanintheus: Southern Milky Way #Australia...</td>
      <td>6</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 22:46:17</td>
      <td>1074007556</td>
      <td>zoomii333</td>
      <td>Janus Sharpe</td>
      <td>2013-01-09 14:56:24</td>
      <td>Clinical Hypnotherapist specialising in all di...</td>
      <td>1534</td>
      <td>1329</td>
      <td>Peterborough, Ontario</td>
      <td>Eastern Time (US &amp; Canada)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>916796848593080320</td>
      <td>RT @theqatarinsider: #Australia in line to tak...</td>
      <td>5</td>
      <td>Infomation Service Provider43</td>
      <td>2017-10-07 22:46:16</td>
      <td>906760003897327617</td>
      <td>asia_active</td>
      <td>Asia Active</td>
      <td>2017-09-10 06:03:26</td>
      <td>Promoting the best articles and retweets about...</td>
      <td>94</td>
      <td>70</td>
      <td>Global</td>
      <td>Caracas</td>
    </tr>
    <tr>
      <th>6</th>
      <td>916796765445246976</td>
      <td>RT @justinbieber: #PurposeTourStadiums #Australia</td>
      <td>57447</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:45:56</td>
      <td>797075565756948484</td>
      <td>Gabyabreu22</td>
      <td>GabyAbreu</td>
      <td>2016-11-11 13:56:38</td>
      <td>👸Belieber \n📽Muser  (Musical.ly) \n🎬YouTuber \...</td>
      <td>174</td>
      <td>765</td>
      <td>São Paulo, Brasil</td>
      <td>None</td>
    </tr>
    <tr>
      <th>7</th>
      <td>916796543499407360</td>
      <td>Laniakea #Campground #Youcamp #NSW #Australia\...</td>
      <td>0</td>
      <td>LaterMedia</td>
      <td>2017-10-07 22:45:03</td>
      <td>818749590</td>
      <td>Wikicamps</td>
      <td>WikiCamps</td>
      <td>2012-09-12 03:33:23</td>
      <td>The original and the best!  A dynamic user gen...</td>
      <td>913</td>
      <td>309</td>
      <td></td>
      <td>Beijing</td>
    </tr>
    <tr>
      <th>8</th>
      <td>916796316411486213</td>
      <td>RT @LeeSunnyBR: [#INSTAGRAM] 07.10.17 | Eu est...</td>
      <td>4</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 22:44:09</td>
      <td>828634301919068161</td>
      <td>hruhae</td>
      <td>kungfu boy⚠️</td>
      <td>2017-02-06 15:59:47</td>
      <td>🌸he's not Superman he must be mama boy🌸</td>
      <td>375</td>
      <td>313</td>
      <td>D-32 ⚠️</td>
      <td>Pacific Time (US &amp; Canada)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>916796311965376512</td>
      <td>#Insiders #Australia contemplates longer Deten...</td>
      <td>1</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 22:44:08</td>
      <td>3029925590</td>
      <td>savillj013</td>
      <td>jsavill</td>
      <td>2015-02-19 12:54:49</td>
      <td>ARCHIVE: Internationalist, #auspol, #qldpol, j...</td>
      <td>737</td>
      <td>2076</td>
      <td>Logan, Queensland, Australia</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1820</th>
      <td>916628467357061120</td>
      <td>RT @SonexStella: [TRANS] Shortly, if you turn ...</td>
      <td>96</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 11:37:11</td>
      <td>104408314</td>
      <td>soshi9014</td>
      <td>S💖NE forever</td>
      <td>2010-01-13 07:03:27</td>
      <td></td>
      <td>145</td>
      <td>62</td>
      <td></td>
      <td>Kuala Lumpur</td>
    </tr>
    <tr>
      <th>1821</th>
      <td>916628346116571136</td>
      <td>RT @MyloveKBS: 이번엔 #케언스 못지않다는 #브리즈번\n여행 대신 화보 ...</td>
      <td>441</td>
      <td>Twitter Web Client</td>
      <td>2017-10-07 11:36:42</td>
      <td>962434338</td>
      <td>CarcassiaZ</td>
      <td>Hakuna Matata</td>
      <td>2012-11-21 13:54:53</td>
      <td>8 years with #Soshi #TYsone  Lovely Fan 10👑 | ...</td>
      <td>58</td>
      <td>228</td>
      <td>House Stark.</td>
      <td>Bangkok</td>
    </tr>
    <tr>
      <th>1822</th>
      <td>916628239770112000</td>
      <td>RT @RFI_English: Could postal survey help the ...</td>
      <td>2</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 11:36:17</td>
      <td>27098486</td>
      <td>FabienJ</td>
      <td>Fabien Jannic</td>
      <td>2009-03-27 21:12:18</td>
      <td>Journaliste radio et web, principalement pour ...</td>
      <td>1058</td>
      <td>1438</td>
      <td>Paris - France</td>
      <td>Eastern Time (US &amp; Canada)</td>
    </tr>
    <tr>
      <th>1823</th>
      <td>916628156051869696</td>
      <td>RT @CharlotdeMan: #Africa #Asia #Australia #An...</td>
      <td>2</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 11:35:57</td>
      <td>1088759970</td>
      <td>CharlotdeMan</td>
      <td>Charlot de Man</td>
      <td>2013-01-14 11:37:38</td>
      <td>#iAmTheOne #DIVINE #Energy #Universe #Touba #S...</td>
      <td>375</td>
      <td>880</td>
      <td></td>
      <td>None</td>
    </tr>
    <tr>
      <th>1824</th>
      <td>916628117011226626</td>
      <td>RT @CharlotdeMan: #Africa #Asia #Australia #An...</td>
      <td>2</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 11:35:47</td>
      <td>1088759970</td>
      <td>CharlotdeMan</td>
      <td>Charlot de Man</td>
      <td>2013-01-14 11:37:38</td>
      <td>#iAmTheOne #DIVINE #Energy #Universe #Touba #S...</td>
      <td>375</td>
      <td>880</td>
      <td></td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>




```python
DataSet.loc[(DataSet['userLocation']=="Melbourne")&(DataSet['userTimezone']=="Melbourne"),:]
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
print("LOCATION")
DataSet["userLocation"].value_counts()
print("TIMEZONE")
DataSet["userTimezone"].value_counts()
```

    LOCATION
    




                                         430
    Australia                             41
    India                                 31
    United States                         29
    Sydney, Australia                     23
    Boston, MA                            22
    Fresno, CA                            20
    New Delhi, India                      15
    Sydney, New South Wales               14
    Alabama, USA                          14
    Florida, USA                          13
    Virginia Beach, VA                    13
    World                                 12
    Melbourne, Australia                  12
    Cary, NC                              10
    London                                10
    Mumbai, India                         10
    Vadodara, India                       10
    brisbane                               8
    australia                              8
    Dallas, TX                             8
    Chennai, India                         8
    Melbourne, Victoria                    8
    Kazakhstan + Russia (Moscow)           7
    Matkaniva                              7
    Canberra, Australia                    7
    United Kingdom                         7
    Victor Harbor                          7
    New Delhi                              7
    UK                                     6
                                        ... 
     India                                 1
    Digital Nomads                         1
    phuket                                 1
    Azores islands                         1
    US /UK /AU                             1
    ziam                                   1
    Jammu And Kashmir                      1
    Goa, India                             1
    The World Is My Oyster                 1
    Britain                                1
    Gold Coast, Qld,  Australia            1
    Duque de Caxias, Brasil                1
    Bunul, Malang                          1
    Hervey Bay, QLD, Australia             1
    Tuticorin                              1
    استراليا - مولبوني                     1
    Macondo                                1
    Atlanta, GA                            1
    Sogeum's cat tower                     1
    Kurdistan, Europe                      1
    Chennai,India                          1
    Los Barriles, Baja Sur Mexico          1
    Toowoomba, QLD, Australia              1
    London & Wales/Mün /Natal Brasil       1
    Peterborough, Ontario                  1
    Canada, Global                         1
    Mission BC Canada                      1
    Bowling Green, KY  USA                 1
    Gungahlin, Canberra                    1
    Dubai U.A.E                            1
    Name: userLocation, Length: 782, dtype: int64



    TIMEZONE
    




    Pacific Time (US & Canada)        226
    London                             75
    New Delhi                          69
    Eastern Time (US & Canada)         68
    Sydney                             59
    Central Time (US & Canada)         45
    Melbourne                          41
    Brisbane                           24
    Amsterdam                          21
    Madrid                             18
    Chennai                            17
    Casablanca                         16
    Brasilia                           15
    Buenos Aires                       14
    Rome                               14
    Mumbai                             12
    Quito                              12
    Arizona                            11
    Asia/Calcutta                      11
    Atlantic Time (Canada)             10
    Hawaii                             10
    Perth                              10
    Athens                             10
    Santiago                           10
    Dublin                             10
    Adelaide                           10
    Mountain Time (US & Canada)         9
    Yakutsk                             9
    Bern                                9
    Bangkok                             9
                                     ... 
    Pretoria                            2
    Midway Island                       1
    Europe/Berlin                       1
    America/Argentina/Buenos_Aires      1
    Europe/Amsterdam                    1
    International Date Line West        1
    Cairo                               1
    Ljubljana                           1
    Vienna                              1
    Australia/Sydney                    1
    Belgrade                            1
    Rangoon                             1
    Tehran                              1
    America/Los_Angeles                 1
    Stockholm                           1
    Tijuana                             1
    Asia/Qatar                          1
    Helsinki                            1
    Lima                                1
    Yerevan                             1
    Azores                              1
    Prague                              1
    Kyiv                                1
    Auckland                            1
    Islamabad                           1
    Mid-Atlantic                        1
    America/New_York                    1
    Kuwait                              1
    America/Mexico_City                 1
    La Paz                              1
    Name: userTimezone, Length: 98, dtype: int64



Timezone is better to look at than Location, because people can input their own Location so it's harder to choose tweets by location, whereas with timezone Sydney, Brisbane, and Melbourne seem to be the only ones that show up.
How many of these tweets are from tourists?


```python
# Removing rows with "None" in "userTimezone"
DataSet = DataSet[DataSet.userTimezone.notnull()]

# Rows remaining
len(DataSet)

# Percentage of rows remaining
#len(DataSet)/2500*100

```




    1037




```python
# Count tweets per time zone for the top 10 time zones
DataSet['userTimezone'].value_counts()
```




    Pacific Time (US & Canada)        226
    London                             75
    New Delhi                          69
    Eastern Time (US & Canada)         68
    Sydney                             59
    Central Time (US & Canada)         45
    Melbourne                          41
    Brisbane                           24
    Amsterdam                          21
    Madrid                             18
    Chennai                            17
    Casablanca                         16
    Brasilia                           15
    Rome                               14
    Buenos Aires                       14
    Mumbai                             12
    Quito                              12
    Asia/Calcutta                      11
    Arizona                            11
    Dublin                             10
    Santiago                           10
    Perth                              10
    Hawaii                             10
    Athens                             10
    Adelaide                           10
    Atlantic Time (Canada)             10
    Bangkok                             9
    Yakutsk                             9
    Mountain Time (US & Canada)         9
    Bern                                9
                                     ... 
    Abu Dhabi                           2
    Australia/Sydney                    1
    Europe/Berlin                       1
    America/Los_Angeles                 1
    Mid-Atlantic                        1
    Stockholm                           1
    Kyiv                                1
    America/New_York                    1
    Tehran                              1
    La Paz                              1
    Rangoon                             1
    Vienna                              1
    Cairo                               1
    International Date Line West        1
    Prague                              1
    Europe/Amsterdam                    1
    Tijuana                             1
    Auckland                            1
    Islamabad                           1
    Midway Island                       1
    America/Argentina/Buenos_Aires      1
    America/Mexico_City                 1
    Azores                              1
    Yerevan                             1
    Kuwait                              1
    Ljubljana                           1
    Belgrade                            1
    Helsinki                            1
    Asia/Qatar                          1
    Lima                                1
    Name: userTimezone, Length: 98, dtype: int64




```python
# Bar Graph of Time Zone data
plt.rcParams['figure.figsize'] = (15, 5)
DataSet['userTimezone'].value_counts().plot(kind='bar')
# Graph Labeling
plt.xlabel('Timezones')
plt.ylabel('Tweet Count')
plt.title('Top 10 Timezones tweeting about #Australia')
```




    <matplotlib.axes._subplots.AxesSubplot object at 0x0000023EC6C82F28>






    <matplotlib.text.Text object at 0x0000023EC6CC4278>






    <matplotlib.text.Text object at 0x0000023EC6CD2400>






    <matplotlib.text.Text object at 0x0000023EC6E39CC0>




```python
sydney = DataSet.loc[DataSet['userTimezone'] == 'Sydney', :] 
sydney.head(2)

brisbane = DataSet.loc[DataSet['userTimezone'] == 'Brisbane',:]  
brisbane.head(2)

melbourne = DataSet.loc[DataSet['userTimezone'] == 'Melbourne',:]
melbourne.head(2)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16</th>
      <td>916795862428168192</td>
      <td>RT @Sophiemcneill: Winner of #NobelPrize2017 @...</td>
      <td>12</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 22:42:21</td>
      <td>17173763</td>
      <td>sparkii</td>
      <td>crina b</td>
      <td>2008-11-05 00:04:34</td>
      <td>Senior Digital Producer/UXer. Former Greenpeac...</td>
      <td>1883</td>
      <td>1950</td>
      <td>Always will be Aboriginal Land</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>23</th>
      <td>916795346440691712</td>
      <td>RT @PaulJurak: Neon Pink Infusion\n#Canberra #...</td>
      <td>5</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:40:18</td>
      <td>530980768</td>
      <td>echidna_paw</td>
      <td>Quasar Yes</td>
      <td>2012-03-20 06:48:14</td>
      <td></td>
      <td>1791</td>
      <td>3530</td>
      <td></td>
      <td>Sydney</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24</th>
      <td>916795341072228357</td>
      <td>#floriade #canberra #spring #flowers #australi...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:40:17</td>
      <td>430624150</td>
      <td>SonyaHeaney</td>
      <td>Sonya Heaney</td>
      <td>2011-12-07 11:38:25</td>
      <td>http://t.co/Px6g5n1A9Z</td>
      <td>737</td>
      <td>1106</td>
      <td>Canberra Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>43</th>
      <td>916794816981118976</td>
      <td>#floriade #canberra #spring #flowers #nature #...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:38:12</td>
      <td>430624150</td>
      <td>SonyaHeaney</td>
      <td>Sonya Heaney</td>
      <td>2011-12-07 11:38:25</td>
      <td>http://t.co/Px6g5n1A9Z</td>
      <td>737</td>
      <td>1106</td>
      <td>Canberra Australia</td>
      <td>Brisbane</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>30</th>
      <td>916795039694467072</td>
      <td>#Communications Business Analyst - LTE / 4G / ...</td>
      <td>0</td>
      <td>dlvr.it</td>
      <td>2017-10-07 22:39:05</td>
      <td>338785232</td>
      <td>PaxusIT</td>
      <td>Paxus Tech + Digital</td>
      <td>2011-07-20 02:49:32</td>
      <td>Looking for a #job in #IT, #digital, #SAP or #...</td>
      <td>2613</td>
      <td>4834</td>
      <td>Australia</td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>31</th>
      <td>916795037853270016</td>
      <td>#Junior Security Analyst: Seeking a Junior Sec...</td>
      <td>0</td>
      <td>dlvr.it</td>
      <td>2017-10-07 22:39:04</td>
      <td>338785232</td>
      <td>PaxusIT</td>
      <td>Paxus Tech + Digital</td>
      <td>2011-07-20 02:49:32</td>
      <td>Looking for a #job in #IT, #digital, #SAP or #...</td>
      <td>2613</td>
      <td>4834</td>
      <td>Australia</td>
      <td>Melbourne</td>
    </tr>
  </tbody>
</table>
</div>




```python
Aust_result = pd.concat([sydney,melbourne,brisbane])
Aust_result
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16</th>
      <td>916795862428168192</td>
      <td>RT @Sophiemcneill: Winner of #NobelPrize2017 @...</td>
      <td>12</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 22:42:21</td>
      <td>17173763</td>
      <td>sparkii</td>
      <td>crina b</td>
      <td>2008-11-05 00:04:34</td>
      <td>Senior Digital Producer/UXer. Former Greenpeac...</td>
      <td>1883</td>
      <td>1950</td>
      <td>Always will be Aboriginal Land</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>23</th>
      <td>916795346440691712</td>
      <td>RT @PaulJurak: Neon Pink Infusion\n#Canberra #...</td>
      <td>5</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:40:18</td>
      <td>530980768</td>
      <td>echidna_paw</td>
      <td>Quasar Yes</td>
      <td>2012-03-20 06:48:14</td>
      <td></td>
      <td>1791</td>
      <td>3530</td>
      <td></td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>53</th>
      <td>916794063935774721</td>
      <td>RT @PaulJurak: Colossal Beginning \n#Canberra ...</td>
      <td>3</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:35:12</td>
      <td>530980768</td>
      <td>echidna_paw</td>
      <td>Quasar Yes</td>
      <td>2012-03-20 06:48:14</td>
      <td></td>
      <td>1791</td>
      <td>3530</td>
      <td></td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>56</th>
      <td>916793835660877824</td>
      <td>RT @Jackthelad1947: Well done to the thousands...</td>
      <td>8</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:34:18</td>
      <td>99367063</td>
      <td>BBBubby77</td>
      <td>No Body</td>
      <td>2009-12-25 21:57:38</td>
      <td>Only I know the trouble you've seen....</td>
      <td>751</td>
      <td>903</td>
      <td></td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>66</th>
      <td>916793269857734657</td>
      <td>Fly away little birdie  #billboard #billboarda...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:32:03</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>69</th>
      <td>916793054891171840</td>
      <td>Please don’t leaf me  #billboard #billboardart...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:31:12</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>73</th>
      <td>916792790004174849</td>
      <td>Deep in the heart of the #BlueMountains is whe...</td>
      <td>0</td>
      <td>Hootsuite</td>
      <td>2017-10-07 22:30:08</td>
      <td>112571375</td>
      <td>scenicworld_aus</td>
      <td>Scenic World</td>
      <td>2010-02-09 00:13:16</td>
      <td>Home of the world's steepest passenger railway...</td>
      <td>4806</td>
      <td>4228</td>
      <td>Blue Mountains, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>74</th>
      <td>916792667215818752</td>
      <td>A berry good dog  #billboard #billboardart #fo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:29:39</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>79</th>
      <td>916792521929445377</td>
      <td>SYDNEY HARBOUR CRUISE WITH LDA....\n#sydney #h...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:29:05</td>
      <td>174803534</td>
      <td>MCJaimeJesus</td>
      <td>Jaime Jesus</td>
      <td>2010-08-04 21:34:45</td>
      <td>Business owner, Latin Entertainer and professi...</td>
      <td>266</td>
      <td>195</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>143</th>
      <td>916786740135907328</td>
      <td>Cool cauli  #billboard #billboardart #food #fo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:06:06</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>161</th>
      <td>916785487167098880</td>
      <td>RT @comradereddy: #Australian people say 'No T...</td>
      <td>3</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 22:01:07</td>
      <td>1349039863</td>
      <td>itzsamya</td>
      <td>Samyamoy</td>
      <td>2013-04-13 11:44:17</td>
      <td>IT professional-SAP Banking Consultant</td>
      <td>295</td>
      <td>266</td>
      <td>Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>164</th>
      <td>916785382850621440</td>
      <td>RT @WildForests: How much representation do #A...</td>
      <td>6</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 22:00:42</td>
      <td>226738150</td>
      <td>FLYFLEDGLINGFLY</td>
      <td>Margaret M Bennett</td>
      <td>2010-12-14 23:20:01</td>
      <td>MAKE Time to smell the Roses, while they're bl...</td>
      <td>1189</td>
      <td>2540</td>
      <td>Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>169</th>
      <td>916785130861137920</td>
      <td>A twist of lime #billboard #billboardart #food...</td>
      <td>1</td>
      <td>Instagram</td>
      <td>2017-10-07 21:59:42</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>182</th>
      <td>916784460179361792</td>
      <td>Fruit and veggie sculptures #billboard #billbo...</td>
      <td>1</td>
      <td>Instagram</td>
      <td>2017-10-07 21:57:02</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>184</th>
      <td>916784237398728705</td>
      <td>You are a sweet heart Fruit #billboard #billbo...</td>
      <td>1</td>
      <td>Instagram</td>
      <td>2017-10-07 21:56:09</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>190</th>
      <td>916783871940730880</td>
      <td>Stairway to juice heaven.... #billboard #billb...</td>
      <td>4</td>
      <td>Instagram</td>
      <td>2017-10-07 21:54:42</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>199</th>
      <td>916783264110608384</td>
      <td>King of the world... or the broccoli #billboar...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:52:17</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>203</th>
      <td>916782998804033536</td>
      <td>Fruit and veggie sculptures #billboard #billbo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:51:14</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>206</th>
      <td>916782713562116097</td>
      <td>Study Loans is the first private #student loan...</td>
      <td>0</td>
      <td>Hootsuite</td>
      <td>2017-10-07 21:50:06</td>
      <td>21282222</td>
      <td>YellCreative</td>
      <td>Yell Creative</td>
      <td>2009-02-19 07:52:35</td>
      <td>Connecting fin services with their customers t...</td>
      <td>585</td>
      <td>974</td>
      <td>Surry Hills, Sydney</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>212</th>
      <td>916782416903077888</td>
      <td>Fruit and veggie sculptures #billboard #billbo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:48:55</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>217</th>
      <td>916781735941230592</td>
      <td>Fruit and veggie sculptures #billboard #billbo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:46:13</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>226</th>
      <td>916780665839935488</td>
      <td>Fruit and veggie sculptures #billboard #billbo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:41:58</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>228</th>
      <td>916780324692070401</td>
      <td>Fruit and veggie sculptures #billboard #billbo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:40:37</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>263</th>
      <td>916777949445214208</td>
      <td>Order up! #cafe #coffee  #dessert #queenspastr...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:31:10</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>267</th>
      <td>916777516370718720</td>
      <td>Cafe couture #cafe #coffee  #dessert #queenspa...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:29:27</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>277</th>
      <td>916776589676785664</td>
      <td>Pull up a seat and stay a while...  #dessert #...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:25:46</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>281</th>
      <td>916776285900218368</td>
      <td>Top day! ☀️😎🏊🏊 #Sunshine #AvocaBeach #Australi...</td>
      <td>0</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 21:24:34</td>
      <td>3108245485</td>
      <td>MrMichaelSharpe</td>
      <td>Michael Sharpe 🇦🇺</td>
      <td>2015-03-26 10:38:59</td>
      <td>Advance Australia</td>
      <td>8281</td>
      <td>8928</td>
      <td>Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>282</th>
      <td>916776251729285122</td>
      <td>Orange bliss!  #dessert #croissant #queenspast...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 21:24:25</td>
      <td>391591862</td>
      <td>shoegalnycblog</td>
      <td>Kaz</td>
      <td>2011-10-15 20:23:58</td>
      <td>Follow me on Instagram: http://t.co/go5SgduRQR</td>
      <td>2009</td>
      <td>1874</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>288</th>
      <td>916775162535600128</td>
      <td>Make runs while the 🌅 is shining! Score big wi...</td>
      <td>0</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 21:20:06</td>
      <td>292118045</td>
      <td>SpartanSportsAU</td>
      <td>Spartan Sports</td>
      <td>2011-05-03 03:57:41</td>
      <td>Spartan is passionate about sport. We develop ...</td>
      <td>11744</td>
      <td>504</td>
      <td>Global</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>336</th>
      <td>916770195145977856</td>
      <td>New Crowdfunding Laws: Australia Still “Way Be...</td>
      <td>0</td>
      <td>Hootsuite</td>
      <td>2017-10-07 21:00:21</td>
      <td>398437134</td>
      <td>SydBizNet</td>
      <td>SydBizNet</td>
      <td>2011-10-26 02:01:33</td>
      <td>Winner: Top 100 Small Business Influencers Awa...</td>
      <td>3423</td>
      <td>3325</td>
      <td>Sydney, Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1563</th>
      <td>916652725617745922</td>
      <td>😱🔥🔥🔥🔥🔥😍🖤💜 #AdamLambert #TheOriginalHigh #Tour ...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 13:13:35</td>
      <td>93153839</td>
      <td>MissSpookiness9</td>
      <td>Magda D ♎️ ^V^</td>
      <td>2009-11-28 09:47:06</td>
      <td>Aspiring photographer📸Movie🎥music🎼junkie AL🎤TJ...</td>
      <td>826</td>
      <td>2440</td>
      <td>Melbourne, Australia</td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>1616</th>
      <td>916647895448805376</td>
      <td>Pokemon DVD (Region 4) Ending Soon on eBay AU ...</td>
      <td>0</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 12:54:23</td>
      <td>2281280671</td>
      <td>NukeAdCo</td>
      <td>Nuke Ad Co ☢</td>
      <td>2014-01-07 23:06:05</td>
      <td>Powerful advertising and media solutions broug...</td>
      <td>2988</td>
      <td>2440</td>
      <td>US /UK /AU</td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>1641</th>
      <td>916645567047929856</td>
      <td>Brick walls.\n#geelong #geelongaustralia #vict...</td>
      <td>0</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 12:45:08</td>
      <td>1406427997</td>
      <td>RiordanSM</td>
      <td>Riordan</td>
      <td>2013-05-06 00:29:08</td>
      <td>Riordan Stewart-McDougall • Australia • Believ...</td>
      <td>43</td>
      <td>105</td>
      <td>Australia</td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>1703</th>
      <td>916639770180149249</td>
      <td>RT @palmboy4444: #Australia says #StopAdani #c...</td>
      <td>7</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 12:22:06</td>
      <td>1670811</td>
      <td>ClownFishTaylor</td>
      <td>Clownfish</td>
      <td>2007-03-20 21:10:08</td>
      <td>Startups, product development, user centered d...</td>
      <td>797</td>
      <td>1347</td>
      <td></td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>1714</th>
      <td>916638151556206592</td>
      <td>What? #Australia https://t.co/Su5ippuYhQ</td>
      <td>0</td>
      <td>Echofon</td>
      <td>2017-10-07 12:15:40</td>
      <td>78787098</td>
      <td>AngelaKorras</td>
      <td>Angela Korras</td>
      <td>2009-10-01 03:13:25</td>
      <td>Freedom for all not just the few, Terrorism wo...</td>
      <td>3687</td>
      <td>3780</td>
      <td>Australia</td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>1790</th>
      <td>916630748148391937</td>
      <td>RT @JanelleBowden: The problems #healthtech an...</td>
      <td>2</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 11:46:15</td>
      <td>823811552381808643</td>
      <td>_IMNIS</td>
      <td>IMNIS</td>
      <td>2017-01-24 08:35:54</td>
      <td>A diverse Industry Mentoring Network fostering...</td>
      <td>1608</td>
      <td>5001</td>
      <td>Australia</td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>24</th>
      <td>916795341072228357</td>
      <td>#floriade #canberra #spring #flowers #australi...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:40:17</td>
      <td>430624150</td>
      <td>SonyaHeaney</td>
      <td>Sonya Heaney</td>
      <td>2011-12-07 11:38:25</td>
      <td>http://t.co/Px6g5n1A9Z</td>
      <td>737</td>
      <td>1106</td>
      <td>Canberra Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>43</th>
      <td>916794816981118976</td>
      <td>#floriade #canberra #spring #flowers #nature #...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:38:12</td>
      <td>430624150</td>
      <td>SonyaHeaney</td>
      <td>Sonya Heaney</td>
      <td>2011-12-07 11:38:25</td>
      <td>http://t.co/Px6g5n1A9Z</td>
      <td>737</td>
      <td>1106</td>
      <td>Canberra Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>76</th>
      <td>916792650119790592</td>
      <td>@AudreyCooke77 @jameshancockABC @abcnews @abcn...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-07 22:29:35</td>
      <td>1411726710</td>
      <td>Chris_E_Qld_Au</td>
      <td>Chris Eastaughffe</td>
      <td>2013-05-08 02:16:00</td>
      <td>Company Director, Investigator, Author.  Exper...</td>
      <td>147</td>
      <td>60</td>
      <td>Queensland, Australia.</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>88</th>
      <td>916791800379166720</td>
      <td>#canberra #floriade #australia #spring #flower...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 22:26:13</td>
      <td>430624150</td>
      <td>SonyaHeaney</td>
      <td>Sonya Heaney</td>
      <td>2011-12-07 11:38:25</td>
      <td>http://t.co/Px6g5n1A9Z</td>
      <td>737</td>
      <td>1106</td>
      <td>Canberra Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>191</th>
      <td>916783805658099718</td>
      <td>@australian WHY is there a backlash for a pers...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-07 21:54:26</td>
      <td>1411726710</td>
      <td>Chris_E_Qld_Au</td>
      <td>Chris Eastaughffe</td>
      <td>2013-05-08 02:16:00</td>
      <td>Company Director, Investigator, Author.  Exper...</td>
      <td>147</td>
      <td>60</td>
      <td>Queensland, Australia.</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>233</th>
      <td>916780208761344000</td>
      <td>RT @ButterflyWrite: #Australia thousands peopl...</td>
      <td>13</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 21:40:09</td>
      <td>485497413</td>
      <td>MinhKular</td>
      <td>JustBlameLabor🏳️‍🌈</td>
      <td>2012-02-07 08:14:00</td>
      <td>#antiracist #VAW #animallover #Unionthug #True...</td>
      <td>9328</td>
      <td>4776</td>
      <td>Cape York and Cairns</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>345</th>
      <td>916768701193613312</td>
      <td>Sharon Curl Leading PNA in Australia. Helping ...</td>
      <td>0</td>
      <td>The Social Jukebox</td>
      <td>2017-10-07 20:54:25</td>
      <td>2848125350</td>
      <td>tagbusiness</td>
      <td>Think&amp;Grow Business</td>
      <td>2014-10-09 02:22:46</td>
      <td>Think and Grow Business. Improving the perform...</td>
      <td>4649</td>
      <td>416</td>
      <td>Brisbane</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>387</th>
      <td>916763355313876992</td>
      <td>RT @Coolmon2009: Things to do in #Australia  h...</td>
      <td>28</td>
      <td>Twitter Web Client</td>
      <td>2017-10-07 20:33:11</td>
      <td>3012906360</td>
      <td>RadugaTourism</td>
      <td>Raduga Tourism</td>
      <td>2015-02-08 03:16:20</td>
      <td>#Gaytravel #Australia Español: https://t.co/SC...</td>
      <td>2182</td>
      <td>2151</td>
      <td>Cairns, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>388</th>
      <td>916763251349716992</td>
      <td>RT @GreenAwakening: #Australia—massive #defore...</td>
      <td>7</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 20:32:46</td>
      <td>2897233640</td>
      <td>watt_shane</td>
      <td>🕳watthefu?#*^!🕳</td>
      <td>2014-11-12 06:34:56</td>
      <td>Im probably gonna r/t th shit outta u !!\nhav ...</td>
      <td>3371</td>
      <td>3156</td>
      <td>Butchulla country</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>389</th>
      <td>916763251291045888</td>
      <td>Mackay Sunrise this morning 🙏🏻🤸‍♀️ #Australia ...</td>
      <td>0</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 20:32:46</td>
      <td>48960532</td>
      <td>Shannon_Clare</td>
      <td>Shannon Clare</td>
      <td>2009-06-20 08:21:52</td>
      <td>ૐ Yoga &amp; Lifestyle Blogger | #Yoga Teacher In ...</td>
      <td>2520</td>
      <td>961</td>
      <td>Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>429</th>
      <td>916757556420333574</td>
      <td>#Airwaves #Menthol #Eucalyptus is one of the m...</td>
      <td>0</td>
      <td>Hootsuite</td>
      <td>2017-10-07 20:10:08</td>
      <td>48929905</td>
      <td>Moo_Lolly_Bar</td>
      <td>Moo-Lolly-Bar</td>
      <td>2009-06-20 04:47:42</td>
      <td>Moo-Lolly-Bar is the best online chocolate, lo...</td>
      <td>1314</td>
      <td>1782</td>
      <td>Sunshine Coast, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>465</th>
      <td>916751915156770816</td>
      <td>RT @BrendanCarton: 29% of new vehicles sold in...</td>
      <td>2</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 19:47:43</td>
      <td>485497413</td>
      <td>MinhKular</td>
      <td>JustBlameLabor🏳️‍🌈</td>
      <td>2012-02-07 08:14:00</td>
      <td>#antiracist #VAW #animallover #Unionthug #True...</td>
      <td>9328</td>
      <td>4776</td>
      <td>Cape York and Cairns</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>708</th>
      <td>916724390011604992</td>
      <td>What #dumb #leaders do! Share if you have had ...</td>
      <td>0</td>
      <td>The Social Jukebox</td>
      <td>2017-10-07 17:58:21</td>
      <td>2848125350</td>
      <td>tagbusiness</td>
      <td>Think&amp;Grow Business</td>
      <td>2014-10-09 02:22:46</td>
      <td>Think and Grow Business. Improving the perform...</td>
      <td>4649</td>
      <td>416</td>
      <td>Brisbane</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>901</th>
      <td>916711502299635712</td>
      <td>Backwash ....by Stuart McAndrew #australia htt...</td>
      <td>0</td>
      <td>smqueue</td>
      <td>2017-10-07 17:07:08</td>
      <td>28039485</td>
      <td>GWPStaff</td>
      <td>GWPstaff</td>
      <td>2009-04-01 03:19:22</td>
      <td>Staff &amp; Friends Site for @GWPStudio</td>
      <td>84691</td>
      <td>51797</td>
      <td>Brisbane, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1570</th>
      <td>916652093351460865</td>
      <td>Backwash ....by Stuart McAndrew #australia htt...</td>
      <td>0</td>
      <td>DEV smqueue</td>
      <td>2017-10-07 13:11:04</td>
      <td>877393542</td>
      <td>smqueue_live</td>
      <td>smqueue_live</td>
      <td>2012-10-13 09:06:49</td>
      <td>Live Test Account One for @smqueue</td>
      <td>1082</td>
      <td>5001</td>
      <td>Brisbane, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1609</th>
      <td>916649162841755648</td>
      <td>#spritz #palmcove #italianstyle #aperol #apero...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-07 12:59:25</td>
      <td>197386056</td>
      <td>alemondo</td>
      <td>Alessandro Mondo</td>
      <td>2010-10-01 10:56:34</td>
      <td>WEB https://t.co/JcEDllH5pf\nPhotographer inte...</td>
      <td>105</td>
      <td>663</td>
      <td>Cairns, Queensland</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1629</th>
      <td>916646831055970305</td>
      <td>RT @photosSMH: Activists at #StopAdani #protes...</td>
      <td>30</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 12:50:09</td>
      <td>1431952093</td>
      <td>GoldCoastNurse</td>
      <td>Gold Coast Nurse</td>
      <td>2013-05-16 02:01:29</td>
      <td>Will always stand up for workers rights and fi...</td>
      <td>2395</td>
      <td>2743</td>
      <td></td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1652</th>
      <td>916644309536997376</td>
      <td>#Cadbury #Chocolate #Fish from #NewZealand is ...</td>
      <td>0</td>
      <td>Hootsuite</td>
      <td>2017-10-07 12:40:08</td>
      <td>48929905</td>
      <td>Moo_Lolly_Bar</td>
      <td>Moo-Lolly-Bar</td>
      <td>2009-06-20 04:47:42</td>
      <td>Moo-Lolly-Bar is the best online chocolate, lo...</td>
      <td>1314</td>
      <td>1782</td>
      <td>Sunshine Coast, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1701</th>
      <td>916640068181176320</td>
      <td>RT @palmboy4444: #Australia says #StopAdani #c...</td>
      <td>7</td>
      <td>Twitter for Android</td>
      <td>2017-10-07 12:23:17</td>
      <td>40365839</td>
      <td>snaglet</td>
      <td>snaglet</td>
      <td>2009-05-15 23:59:27</td>
      <td>consumerism is finished; why buy when sharing ...</td>
      <td>1348</td>
      <td>3892</td>
      <td>Valhalla, Queensland,  Oz</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1730</th>
      <td>916636775870861313</td>
      <td>Top 10 Most Popular #Nestle #Chocolate Bars in...</td>
      <td>0</td>
      <td>Hootsuite</td>
      <td>2017-10-07 12:10:12</td>
      <td>48929905</td>
      <td>Moo_Lolly_Bar</td>
      <td>Moo-Lolly-Bar</td>
      <td>2009-06-20 04:47:42</td>
      <td>Moo-Lolly-Bar is the best online chocolate, lo...</td>
      <td>1314</td>
      <td>1782</td>
      <td>Sunshine Coast, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1741</th>
      <td>916635672290529280</td>
      <td>#Australia says #StopAdani #coal mine\n#Queens...</td>
      <td>1</td>
      <td>Twitter Web Client</td>
      <td>2017-10-07 12:05:49</td>
      <td>134012695</td>
      <td>palmboy4444</td>
      <td>Phil Browne</td>
      <td>2010-04-17 06:34:56</td>
      <td>Advocate for a #secular #sustainable society a...</td>
      <td>1030</td>
      <td>137</td>
      <td>Brisbane, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1769</th>
      <td>916633709008187392</td>
      <td>#Australia says #StopAdani #coal mine\n#Queens...</td>
      <td>7</td>
      <td>Twitter Web Client</td>
      <td>2017-10-07 11:58:01</td>
      <td>134012695</td>
      <td>palmboy4444</td>
      <td>Phil Browne</td>
      <td>2010-04-17 06:34:56</td>
      <td>Advocate for a #secular #sustainable society a...</td>
      <td>1030</td>
      <td>137</td>
      <td>Brisbane, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1809</th>
      <td>916629207748370434</td>
      <td>Top 10 #JellyBelly flavours for #Weddings in #...</td>
      <td>0</td>
      <td>Hootsuite</td>
      <td>2017-10-07 11:40:07</td>
      <td>48929905</td>
      <td>Moo_Lolly_Bar</td>
      <td>Moo-Lolly-Bar</td>
      <td>2009-06-20 04:47:42</td>
      <td>Moo-Lolly-Bar is the best online chocolate, lo...</td>
      <td>1314</td>
      <td>1782</td>
      <td>Sunshine Coast, Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>1817</th>
      <td>916628840054525952</td>
      <td>#SpiderManHomecoming is the best #Spiderman so...</td>
      <td>0</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-07 11:38:40</td>
      <td>2959187234</td>
      <td>SareSommer</td>
      <td>Sare Sommer</td>
      <td>2015-01-05 05:11:38</td>
      <td>Trying to get into the music/film industry in ...</td>
      <td>33</td>
      <td>74</td>
      <td>Australia</td>
      <td>Brisbane</td>
    </tr>
  </tbody>
</table>
<p>124 rows × 14 columns</p>
</div>




```python
# TWEETS 212,217,218 ARE THE SAME <-- Posted by the same person a couple of minutes apart.
    # They have the same text EXCEPT for the url at the end 
    # They have different tweetIDs 
        # is there any other way to find duplicate tweets like this?
Aust_result['tweetText'][212]
Aust_result['tweetID'][212]

Aust_result['tweetText'][217]
Aust_result['tweetID'][217]
```




    'Fruit and veggie sculptures #billboard #billboardart #food #foodart #Sydney #Australia #travel… https://t.co/L6T9CB3Za1'






    916782416903077888






    'Fruit and veggie sculptures #billboard #billboardart #food #foodart #Sydney #Australia #travel… https://t.co/rXmy5lvPjY'






    916781735941230592




```python
Aust_result['tweetText']
```




    16      RT @Sophiemcneill: Winner of #NobelPrize2017 @...
    23      RT @PaulJurak: Neon Pink Infusion\n#Canberra #...
    53      RT @PaulJurak: Colossal Beginning \n#Canberra ...
    56      RT @Jackthelad1947: Well done to the thousands...
    66      Fly away little birdie  #billboard #billboarda...
    69      Please don’t leaf me  #billboard #billboardart...
    73      Deep in the heart of the #BlueMountains is whe...
    74      A berry good dog  #billboard #billboardart #fo...
    79      SYDNEY HARBOUR CRUISE WITH LDA....\n#sydney #h...
    143     Cool cauli  #billboard #billboardart #food #fo...
    161     RT @comradereddy: #Australian people say 'No T...
    164     RT @WildForests: How much representation do #A...
    169     A twist of lime #billboard #billboardart #food...
    182     Fruit and veggie sculptures #billboard #billbo...
    184     You are a sweet heart Fruit #billboard #billbo...
    190     Stairway to juice heaven.... #billboard #billb...
    199     King of the world... or the broccoli #billboar...
    203     Fruit and veggie sculptures #billboard #billbo...
    206     Study Loans is the first private #student loan...
    212     Fruit and veggie sculptures #billboard #billbo...
    217     Fruit and veggie sculptures #billboard #billbo...
    226     Fruit and veggie sculptures #billboard #billbo...
    228     Fruit and veggie sculptures #billboard #billbo...
    263     Order up! #cafe #coffee  #dessert #queenspastr...
    267     Cafe couture #cafe #coffee  #dessert #queenspa...
    277     Pull up a seat and stay a while...  #dessert #...
    281     Top day! ☀️😎🏊🏊 #Sunshine #AvocaBeach #Australi...
    282     Orange bliss!  #dessert #croissant #queenspast...
    288     Make runs while the 🌅 is shining! Score big wi...
    336     New Crowdfunding Laws: Australia Still “Way Be...
                                  ...                        
    1563    😱🔥🔥🔥🔥🔥😍🖤💜 #AdamLambert #TheOriginalHigh #Tour ...
    1616    Pokemon DVD (Region 4) Ending Soon on eBay AU ...
    1641    Brick walls.\n#geelong #geelongaustralia #vict...
    1703    RT @palmboy4444: #Australia says #StopAdani #c...
    1714             What? #Australia https://t.co/Su5ippuYhQ
    1790    RT @JanelleBowden: The problems #healthtech an...
    24      #floriade #canberra #spring #flowers #australi...
    43      #floriade #canberra #spring #flowers #nature #...
    76      @AudreyCooke77 @jameshancockABC @abcnews @abcn...
    88      #canberra #floriade #australia #spring #flower...
    191     @australian WHY is there a backlash for a pers...
    233     RT @ButterflyWrite: #Australia thousands peopl...
    345     Sharon Curl Leading PNA in Australia. Helping ...
    387     RT @Coolmon2009: Things to do in #Australia  h...
    388     RT @GreenAwakening: #Australia—massive #defore...
    389     Mackay Sunrise this morning 🙏🏻🤸‍♀️ #Australia ...
    429     #Airwaves #Menthol #Eucalyptus is one of the m...
    465     RT @BrendanCarton: 29% of new vehicles sold in...
    708     What #dumb #leaders do! Share if you have had ...
    901     Backwash ....by Stuart McAndrew #australia htt...
    1570    Backwash ....by Stuart McAndrew #australia htt...
    1609    #spritz #palmcove #italianstyle #aperol #apero...
    1629    RT @photosSMH: Activists at #StopAdani #protes...
    1652    #Cadbury #Chocolate #Fish from #NewZealand is ...
    1701    RT @palmboy4444: #Australia says #StopAdani #c...
    1730    Top 10 Most Popular #Nestle #Chocolate Bars in...
    1741    #Australia says #StopAdani #coal mine\n#Queens...
    1769    #Australia says #StopAdani #coal mine\n#Queens...
    1809    Top 10 #JellyBelly flavours for #Weddings in #...
    1817    #SpiderManHomecoming is the best #Spiderman so...
    Name: tweetText, Length: 124, dtype: object




```python
Aust_result.to_csv("Australia_Tweets.csv")
```

## #Aussie


```python
# Search for '#Aussie'
aussie_search = api.search(q='%23Aussie')
len(aussie_search)
```




    15




```python
aussie_results = []

#Get the first 5000 items based on the search query
for tweet in tweepy.Cursor(api.search, q='%23Aussie').items(2500):
    aussie_results.append(tweet)

# Verify the number of items returned
print(len(aussie_results))
```

    2500
    


```python
# Checking for duplicate Tweets
aussie_tweet_ids=[x.id for x in aussie_results]
aussie_orig_tweet_ids=set(aussie_tweet_ids)
len(aussie_tweet_ids) == len(aussie_orig_tweet_ids)
len(aussie_tweet_ids)
```




    True






    2500




```python
tweet_texts2=[]
for x in aussie_results:
    if x.text not in tweet_texts2:
        tweet_texts2.append(x.text)
    else:
        aussie_results.remove(x)
        
len(aussie_results)
```




    1829




```python
#Pass the tweets list to 'toDataFrame' to create the DataFrame
Aussie_df = toDataFrame(aussie_results)
Aussie_df.head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>917111776096919552</td>
      <td>#Aussie #Diydiom of the day: scratchy: greitas...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-08 19:37:41</td>
      <td>88822659</td>
      <td>IdiomOfOz</td>
      <td>Jake Jacobs</td>
      <td>2009-11-10 01:50:17</td>
      <td>Starving traveler and middle-aged humour autho...</td>
      <td>1520</td>
      <td>1984</td>
      <td>Parker, Colorado</td>
      <td>Mountain Time (US &amp; Canada)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>917111114952929280</td>
      <td>#Aussie #Idiom of the Day: scratchy: natychmia...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-08 19:35:03</td>
      <td>88822659</td>
      <td>IdiomOfOz</td>
      <td>Jake Jacobs</td>
      <td>2009-11-10 01:50:17</td>
      <td>Starving traveler and middle-aged humour autho...</td>
      <td>1520</td>
      <td>1984</td>
      <td>Parker, Colorado</td>
      <td>Mountain Time (US &amp; Canada)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>917110724463271936</td>
      <td>Enjoying my little Birthday Puppy!🎂🎶🎉🎶#puppylo...</td>
      <td>0</td>
      <td>Instagram</td>
      <td>2017-10-08 19:33:30</td>
      <td>226204701</td>
      <td>dmac108</td>
      <td>Diana McCready</td>
      <td>2010-12-13 15:56:20</td>
      <td>Life is not measured by the breaths we take, b...</td>
      <td>209</td>
      <td>560</td>
      <td>Minnesota</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>917110695111442432</td>
      <td>#Aussie #Idiom of the Day: scratchy: мгновенны...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-08 19:33:23</td>
      <td>88822659</td>
      <td>IdiomOfOz</td>
      <td>Jake Jacobs</td>
      <td>2009-11-10 01:50:17</td>
      <td>Starving traveler and middle-aged humour autho...</td>
      <td>1520</td>
      <td>1984</td>
      <td>Parker, Colorado</td>
      <td>Mountain Time (US &amp; Canada)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>917110220849012736</td>
      <td>#Aussie #Idiom of the Day: scratchy: Un boleto...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-08 19:31:30</td>
      <td>88822659</td>
      <td>IdiomOfOz</td>
      <td>Jake Jacobs</td>
      <td>2009-11-10 01:50:17</td>
      <td>Starving traveler and middle-aged humour autho...</td>
      <td>1520</td>
      <td>1984</td>
      <td>Parker, Colorado</td>
      <td>Mountain Time (US &amp; Canada)</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Removing rows with "None" in "userTimezone"
Aussie_df = Aussie_df[Aussie_df.userTimezone.notnull()]

# Rows remaining
len(Aussie_df)

# Percentage of rows remaining
len(Aussie_df)/100*100

# Lost about 1/2 of the tweets
```




    1018






    1018.0




```python
Aussie_df["userTimezone"].value_counts()
```




    Pacific Time (US & Canada)     233
    Melbourne                      116
    Eastern Time (US & Canada)      98
    Sydney                          78
    Brisbane                        57
    Central Time (US & Canada)      57
    London                          50
    Mountain Time (US & Canada)     35
    Hawaii                          25
    Adelaide                        21
    Athens                          13
    Beijing                         13
    Santiago                        12
    Atlantic Time (Canada)          11
    Brasilia                        11
    Amsterdam                       11
    Perth                           10
    New Delhi                        9
    Madrid                           9
    Rome                             8
    Wellington                       7
    Buenos Aires                     7
    Alaska                           7
    Berlin                           6
    Tokyo                            6
    Greenland                        6
    Quito                            6
    Ljubljana                        5
    Canberra                         5
    New Caledonia                    5
                                  ... 
    Solomon Is.                      2
    Riyadh                           2
    Edinburgh                        2
    Abu Dhabi                        2
    Casablanca                       2
    Kuala Lumpur                     2
    Auckland                         2
    America/Chicago                  1
    West Central Africa              1
    Stockholm                        1
    Hobart                           1
    Mid-Atlantic                     1
    Brussels                         1
    Kiev                             1
    America/Denver                   1
    Central America                  1
    Pretoria                         1
    Monterrey                        1
    America/Detroit                  1
    Warsaw                           1
    America/Los_Angeles              1
    Copenhagen                       1
    Irkutsk                          1
    Europe/London                    1
    Samoa                            1
    Bern                             1
    Europe/Madrid                    1
    Karachi                          1
    Mexico City                      1
    Singapore                        1
    Name: userTimezone, Length: 72, dtype: int64




```python
sydney_aussie = Aussie_df.loc[Aussie_df['userTimezone'] == 'Sydney', :] 
sydney_aussie.head(2)

brisbane_aussie = Aussie_df.loc[Aussie_df['userTimezone'] == 'Brisbane',:]  
brisbane_aussie.head(2)

melbourne_aussie = Aussie_df.loc[Aussie_df['userTimezone'] == 'Melbourne',:]
melbourne_aussie.head(2)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <td>916931318092513282</td>
      <td>@JeremyPalmer7 @Jens62622095 @SteveKubota @Str...</td>
      <td>6</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-08 07:40:36</td>
      <td>275622946</td>
      <td>YumchaAddict</td>
      <td>Yumcha Addict</td>
      <td>2011-04-01 17:12:53</td>
      <td>Aussie Foodie busy blogging, tweeting pics &amp; r...</td>
      <td>16463</td>
      <td>8019</td>
      <td>Sydney Australia</td>
      <td>Sydney</td>
    </tr>
    <tr>
      <th>151</th>
      <td>916844733900611584</td>
      <td>RT @jephilip: Nathan Walker introduced as the ...</td>
      <td>10</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-08 01:56:33</td>
      <td>379623158</td>
      <td>Goto919</td>
      <td>David Atkins</td>
      <td>2011-09-25 08:27:01</td>
      <td>Like SA Redbacks, Sydney Thunder, Cronulla Sha...</td>
      <td>1472</td>
      <td>4821</td>
      <td>Sydney</td>
      <td>Sydney</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>53</th>
      <td>917031389127512064</td>
      <td>A lil bit more #naked #snap #nude #amateur #au...</td>
      <td>1</td>
      <td>Twitter for iPhone</td>
      <td>2017-10-08 14:18:15</td>
      <td>815566364538568705</td>
      <td>aussie_azza</td>
      <td>aussie_azza</td>
      <td>2017-01-01 14:32:28</td>
      <td>Shy guy who doesn't mind showing off for my fa...</td>
      <td>637</td>
      <td>326</td>
      <td>Australia</td>
      <td>Brisbane</td>
    </tr>
    <tr>
      <th>73</th>
      <td>916983765859164161</td>
      <td>#Aussie #outlander fans does Netflix screen it...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-08 11:09:01</td>
      <td>2470351674</td>
      <td>TravelBugWithin</td>
      <td>Jennifer Johnston</td>
      <td>2014-04-30 04:56:19</td>
      <td>Aussie freelance writer sometimes blogger. A c...</td>
      <td>582</td>
      <td>807</td>
      <td>Brisbane, Australia.</td>
      <td>Brisbane</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tweetID</th>
      <th>tweetText</th>
      <th>tweetRetweetCt</th>
      <th>tweetSource</th>
      <th>tweetCreated</th>
      <th>userID</th>
      <th>userScreen</th>
      <th>userName</th>
      <th>userCreateDt</th>
      <th>userDesc</th>
      <th>userFollowerCt</th>
      <th>userFriendsCt</th>
      <th>userLocation</th>
      <th>userTimezone</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>55</th>
      <td>917020426215219200</td>
      <td>Mathew Lobb from #Vodafone blames SLOW #Aussie...</td>
      <td>0</td>
      <td>Twitter Web Client</td>
      <td>2017-10-08 13:34:41</td>
      <td>59488559</td>
      <td>Girrali</td>
      <td>Girrali 😎</td>
      <td>2009-07-23 15:03:39</td>
      <td>🦎 Murrumbidgee Koori 👣 Environmental 🍃🔬 Scient...</td>
      <td>1142</td>
      <td>639</td>
      <td>🦎 Murrumbidgee Wiradjuri</td>
      <td>Melbourne</td>
    </tr>
    <tr>
      <th>85</th>
      <td>916961754533396480</td>
      <td>Ruskie Pierogi - Potato and Cheese ... #Recipe...</td>
      <td>0</td>
      <td>autopostaussietaste</td>
      <td>2017-10-08 09:41:33</td>
      <td>1335982496</td>
      <td>cooking_r</td>
      <td>The Taste of Aussie</td>
      <td>2013-04-08 07:26:10</td>
      <td>At The Taste of Aussie we love to cook and tha...</td>
      <td>1091</td>
      <td>415</td>
      <td>Melbourne, Australia</td>
      <td>Melbourne</td>
    </tr>
  </tbody>
</table>
</div>




```python
Aussie_result=pd.concat([sydney_aussie,brisbane_aussie,melbourne_aussie])
# result = pd.concat([Aust_result,Aussie_result])
# result.head(5)
```


```python
# result.to_csv("Australia_Tweets.csv")
```


```python
Aussie_result.to_csv("Australia_Tweets.csv",mode="a")
```
