## Python Code

```markdown
from instapy import InstaPy
import json
import getpass
import os
from time import sleep

os.system('CLS')
#get stored tables
with open('data.txt') as json_file:
	data = json.load(json_file)
input("WELCOME TO THE PYTHON INSTAGRAM BOT")

os.system('CLS')

#user credentials
insta_username = input('INSERT USERNAME: ')
insta_password = getpass.getpass('INSERT PASSWORD: ')

os.system('CLS')
tag_array = data['tags']
comments_array = data['comments']

#set or change tags
print('TAGS:')
print(*tag_array, sep=' ')
if (input("\nDo you want to change the current tags of the bot? y or ENTER ") == "y"):
	tag_array = input('Insert new tags: ').split()

os.system('CLS')

#set or change comments
print('COMMENTS:')
print(*comments_array, sep=' ')
if (input("\nDo you want to change the current comments of the bot? y or ENTER ") == "y"):
	comments_array.clear()
	number = input('\nHow many comments?: ')
	for i in range(int(number)):
		comments_array.append(input('Tag ' + str(i + 1) + ': '))
os.system('CLS')

data['tags'] = tag_array
data['comments'] = comments_array


#store tags and comments values
with open('data.txt', 'w') as outfile:
	json.dump(data, outfile)
print('\nSTORED: ' + str(data))
sleep(1)
print('\nStarting main bot process')
sleep(1)
os.system('CLS')


session = InstaPy(username=insta_username, password=insta_password)
session.login()

# set up all the settings
session.set_relationship_bounds(enabled=True,
                                potency_ratio=-1.28,
                                delimit_by_numbers=True,
                                max_followers=8000,
                                max_following=9000,
                                min_followers=45,
                                min_following=77)
session.set_do_follow(True, percentage=90)
session.set_do_comment(True, percentage=98)
session.set_comments(comments_array)
session.set_dont_like(["naked", "nsfw"])

# do the actual liking
session.like_by_tags(tag_array, amount=25)

# end the bot session
session.end()
```


