# -*- coding: utf-8 -*-
from datetime import datetime


def get_first_name():
    name = 'Nobody'
    if auth.user:
        name = auth.user.first_name
    return name
def get_email():
    if auth.user:
        return auth.user.email
    else:
        return 'None'
def name_of(user): return '%(first_name)s %(last_name)s' % user

#http://www.smogon.com/forums/threads/excel-pokedex-v5-14-smogon-tiers-and-legal-dw-abilities-here-outdated.102714/
POKEMON = ['Any','pikachu','charmander','squirtle', 'bulbasaur']
#NATURES = [db.bboard.import_from_csv_file(open(os.path.join(request.folder, 'private','natures.txt')))]
NATURES = ['Hardy','Lonely','Adamant','Naughty','Brave',
           'Bold','Docile','Impish','Lax','Relaxed',
           'Modest','Mild','Bashful','Rash','Quiet',
           'Calm','Gentle','Careful','Quirky','Sassy',
           'Timid','Hasty','Jolly','Naive','Serious']

db.define_table('bboard',
                Field('title'),
                Field('user_id', db.auth_user),
                Field('name'),
                Field('date_posted', 'datetime'),
                Field('pokemon'),
                Field('shiny', 'boolean',default = False),
                Field('user_id', db.auth_user),
                Field('email'),
                Field('levelFT'),
                Field('gender'),
                Field('ability'),
                Field('nature'),
                Field('ivs'),
                #Field('LF'),
                Field('bbmessage', 'text'),
                Field('available', 'boolean'),
                )

db.define_table('reply',
               Field('bboard_id', 'reference bboard',requires = IS_IN_DB(db,db.bboard.id, '%(title)s')),
               Field('user_id', db.auth_user),
               Field('date_posted', 'datetime', writable = False),
               Field('body', 'text', requires = IS_NOT_EMPTY()),
               )

#title
db.bboard.title.label = 'Looking For'
db.bboard.title.required = True
#user
db.bboard.user_id.default = auth.user_id
db.bboard.user_id.writable = False#db.bboard.user_id.readable = False
db.reply.user_id.default = auth.user_id
db.reply.user_id.writable = False
#readable
db.bboard.id.readable = False
#message
db.bboard.bbmessage.label = 'Message'
#name
db.bboard.name.default = get_first_name()
db.bboard.name.writable = False
db.bboard.name.readable = False
#date
db.bboard.date_posted.default = datetime.utcnow()
db.bboard.date_posted.writable = False
db.bboard.date_posted.readable = False
db.reply.date_posted.default = datetime.utcnow()
db.reply.date_posted.writable = False
db.reply.date_posted.readable = False
#email
db.bboard.email.default = get_email()
db.bboard.email.writable = False
db.bboard.email.readable = False
db.bboard.email.requires = IS_EMAIL()
#Pokemon
#db.bboard.pokemon.requires = IS_IN_SET(POKEMON)
#db.bboard.pokemon.default = POKEMON[1]
db.bboard.pokemon.required = True
db.bboard.pokemon.label = 'Pokemon for trade'

#db.bboard.LF.readable = True
#db.bboard.LF.requires = IS_IN_SET(POKEMON)
#db.bboard.LF.default = POKEMON[0]
#db.bboard.LF.label = 'Pokemon wanted'
#level
db.bboard.levelFT.label = 'level'
db.bboard.levelFT.requires = IS_INT_IN_RANGE(1, 101,error_message='Please enter a valid level.')
#gender
db.bboard.gender.requires = IS_IN_SET(['female', 'male', 'None'])
db.bboard.gender.required = True
#natures
db.bboard.nature.requires = IS_IN_SET(NATURES, zero=None)
db.bboard.nature.required = True
#available
db.bboard.available.default = True
db.bboard.available.required = True
#error messages
db.bboard.title.requires = IS_NOT_EMPTY(error_message='Enter a title for your listing')
db.bboard.bbmessage.requires = IS_NOT_EMPTY(error_message='Enter a body for your listing')
#db.bboard.phone.requires = IS_NOT_EMPTY(error_message='Enter a valid phone number')
#db.bboard.price.requires = IS_FLOAT_IN_RANGE(0, 100000.0, error_message='The price should be in the range 0..100000')
