title: Detailed audio field rules
id: fieldrules
source_file: downloadaudio/get_fields.py
type: subpage
ankiweb_id: 3100585138
parent: Download audio
extra_jq_script: audio_tips.js

In most cases – including learning Japanese or Chinese with the
[standard](https://ankiweb.net/shared/info/3918629684)
[add-ons](https://ankiweb.net/shared/info/3448800906) installed –
adding a field “Audio” to the note and to at least one side of a card
is enough, but more sophisticated use of the add-on is also possible.

This page describes how the add-on matches audio and text fields and
gives examples on how to use more than one pronunciation per note.

## Fields rules

The download mechanism uses these rules to match audio fields to text
fields:

For most downloaders, plain text is used. The rules to find the source
fields are:

* When there is a field called
  <ul>
    <li>“Audio” or</li>
    <li>“Sound”,</li>
  </ul>
  the add-on looks for a field called
  <ul>
    <li>“Expression” or</li>
    <li>“Front” or</li>
  </ul>
  or for a field with the names of a language where there is a chance of
  downloading words spoken by humans (as opposed to the GoogleTTS
  robot):
  <ul>
    <li>Deutsch</li>
    <li>English</li>
    <li>Español</li>
    <li>Français</li>
    <li>French</li>
    <li>German</li>
    <li>Japanese</li>
    <li>Spanish</li>
    <li>日本語</li>
    <li>漢字</li>
  </ul>
* For fields where “Audio” or “Sound” is a substring, this word is
  removed and the rest used to look for a field. For example, to get
  pronunciations for a field called “Example”, you should add a field
  named “Example Audio” (or “Audio Example”). When downloading, the
  add-on will find the field “Example Audio”, strip the “Audio”, clean
  up the space to get “Example” and look for that field to get the
  text.

To get Japanese pronunciations from
[JapanesePod101.com](http://japanesepod101.com) or Chinese
pronunciations from [LEO.org](http://leo.org) there has to be the
reading stored in the note. The detailed rules are:

* When there is a field called
  <ul>
    <li>“Audio” or</li>
    <li>“Sound”,</li>
  </ul>
  the add-on looks for a field called
  <ul>
    <li>“Reading”,</li>
    <li>“Kana”,</li>
    <li>「かな」,</li>
    <li>「仮名”」,</li>
    <li>“<span class="qtbase hanzipinyin">Hanzi</span>” or</li>
    <li>“Pinyin”.</li>
  </ul>
* The sub-string rule is different for this case. For fields where
  “Audio” or “Sound” is a sub-string, this word is not removed, but
  the add-on looks for fields where that word has been
  *replaced* with  one from the “Reading” list. For example, when
  there is a field called “Japanese Reading”, add a field “Japanese
  Audio” to download from the reading field.

All of these field names are not case sensitive. For example, “expression”,
“FRONT” &c. will all work.

The field names are defined in the lists in the file
“[`downloadaudio/get_fields.py`](https://github.com/ospalh/anki-addons/blob/master/downloadaudio/get_fields.py)”
in the add-ons folder. That folder can be displayed through the
“Tools/Add-ons/Open Add-ons Folder...” menu item.

## Examples

I use complex note types with many fields in my personal
collection. Field lists from these models can be used to demonstrate
real-life use of these rules.

### Model “Standard — Japanese”

My main Japanese vocabulary model has <span class="qtbase
morefields">these fields</span>:

* Expression
* Reading
* Deutsch
* Zusatz
* Audio
* 例文
* 例文 Audio

Applying the rules means that:

* The plain rule matches the field  “Expression” to the field
  “Audio”. The GoogleTTS downloader will work from the expression and
  download into the audio field.
* The readings rule matches the field  “Reading” to the field
  “Audio”. The Japanesepod downloader will work from the reading and
  download into the audio field, too.
* The plain substring rule matches the field “”例文” to the field
  “例文 Audio”
* For the fields “Deutsch” and “Zusatz” (and the audio fields
  themselves), nothing is downloaded.

### Model “Land, state etc.”

For my world-wide geography deck, i use  <span class="qtbase
morefields">the fields</span>:

* CountryName
* CountryName_Audio
* Capital
* CapitalName_Audio
* Map
* Flag
* Inhabitants_Scalar
* Area_Scalar
* NameAlternative
* NameAlternative_Audio
* CapitalAlternative
* CapitalAlternative_Audio

Here only the plain substring rule matches. The add-on tries to get
audio for these field pairs:

* CountryName → CountryName_Audio
* Capital → Capital_Audio
* NameAlternative → NameAlternative_Audio
* CapitalAlternative → CapitalAlternative_Audio


### Model “都道府県 – Japanese”

Here some of the  fields are:

* Präfektur_ローマ字
* 都道府県
* 都道府県_Reading
* 都道府県_Audio
* Nummer
* Einwohner
* Fläche
* Karte

Here the plain substring and the reading substring rules match:

* The plain substring rule matches the field  “都道府県” to the field
  “都道府県_Audio”.
* The readings substring rule matches the field  “都道府県_Reading” to the field
  “都道府県_Audio”.

Here, too, pronunciations from different source texts are downloaded
to the same field


## Card templates

This page does not discuss in detail what to do with the audio
data. Don’t forget to add the audio fields to some card templates. Be
creative.