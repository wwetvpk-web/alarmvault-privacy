---
title: AlarmVault Privacy Policy
description: Privacy policy for the AlarmVault Android app
---

# AlarmVault — Privacy Policy

**Applies to:** AlarmVault for Android (package `com.sgot.alarmvault`)


**Effective date:** 24 September 2026 · **Applies to app version:** 1.3

## In short

AlarmVault keeps your data on your device. It has no account, no sign-in and no server behind it,
and it does not send your alarm settings, your Secure Box contents or your Apps Box list anywhere.

The only information AlarmVault sends off the device is approximate location for the optional
weather section, and only if you allow it. If you use Send feedback, your own email app opens
with a draft that you write and send yourself.

## Introduction

AlarmVault is an Android app that combines an alarm clock with **Secure Box**, a private area for
files and notes that are encrypted on the device, and **Apps Box**, a separate protected area with
its own lock.

This policy describes how the app handles information as it works today. The app runs entirely on
your device: there is no account to create, nothing to sign in to, and no service operated on your
behalf.

## Information and data the app handles

The app handles only what you give it or what it needs in order to work:

- **Alarm settings** — for each alarm you create: its time, whether it is on, its name, which days
  of the week it repeats on, vibration, the snooze length, and the ringtone or audio file you
  choose. A chosen audio file is stored as a reference to that file, not as a copy of it.
- **Items you add to Secure Box** — videos, photos, PDFs and other files.
- **Notes you write in Secure Box** — their title and body.
- **Security material** — a salted verifier for your PIN, password or pattern and for your Recovery
  Key. Neither the credential nor the Recovery Key itself is stored.
- **Apps Box** — the package names of the apps you have imported.
- **Weather** — if you allow it, an approximate location used only to look up current conditions
  for the Home screen, plus the last reading cached for about an hour. No location history is kept.

To let you choose apps in Apps Box, the app asks Android for the list of installed apps that have a
launcher icon. That list is read on the device to display it, and only the package names you import
are saved.

The app does not ask for your name, email address, phone number or contacts, and it has no profile
or account attached to you. Approximate location is used only for the optional weather section
described below, and only with your permission.

## How data is stored

Everything is kept in the app's own private storage area on the device:

- Encrypted Secure Box files, in the app's private files directory.
- A local database holding alarm settings, note contents in encrypted form, and metadata for Secure
  Box items.
- Local preference files holding the security verifiers and the Apps Box list.
- A local preference file recording which shortcuts you put on the AlarmVault Home screen and which
  of the starter ones you removed, so your layout survives a restart.
- A local count of how many times you have opened each app from AlarmVault, used only to put the
  ones you open most at the top of the app drawer. It is not the phone-wide usage statistics, it
  covers only taps inside AlarmVault, and it never leaves the device.
- A local preference file recording whether Secure Box keeps its contents blurred until you
  touch them.
- A local preference file holding the last weather reading — a temperature and a condition word —
  for about an hour. Your coordinates are not stored.

Android keeps this private storage isolated from other apps. Nothing is written to shared or public
storage unless you explicitly export it.

## Secure Box and encryption

Files added to Secure Box are encrypted with **AES-256 in GCM mode**. The encryption key is
generated inside the **Android Keystore** and is not exportable, so it cannot be read out of the
device. Note titles and bodies are encrypted the same way.

Each encrypted file carries an authentication tag that is verified on every read, so a corrupted or
altered file is rejected instead of being shown in part.

Some information is kept unencrypted as ordinary metadata in the app's private local database: an
item's file name, file type, size, the date it was imported, and a checksum used to recognise a
duplicate import.

To play a video or open a PDF, the app writes a temporary decrypted copy into its own private
cache. The same happens briefly for each video shown in the Secure Box list, so a picture from
the video can be used in place of a filename; that copy is deleted as soon as the picture has
been taken. A viewer copy is deleted when you close the viewer, and anything left behind by an
unexpected shutdown is cleared the next time the app starts. Photos are decrypted in memory and
are not written to disk in readable form.

Opening a ZIP, RAR or 7z file in Secure Box works the same way, because those formats have to be
read back and forth rather than straight through: the archive is decrypted into that same private
cache, its contents are encrypted into Secure Box one at a time as they come out, and the
temporary copy is deleted when the work finishes, including when it fails part way. Compressing
files into a new ZIP does the same in reverse. That cache belongs to AlarmVault alone; no other
app on the phone can read it, and nothing is written anywhere you have not asked for.

This is local at-rest encryption. It is deliberately **not** described as end-to-end encryption,
because there is no remote party involved.

## Authentication and security

- Secure Box is protected by a PIN, password or pattern that you choose. It is never stored. Only a
  salted **PBKDF2-HMAC-SHA256** verifier is saved, and unlocking compares against that verifier.
- Repeated incorrect attempts trigger a delay that grows with each further failure.
- Biometric unlock is optional and uses Android's own biometric prompt. The app never receives your
  fingerprint or face data; Android only reports whether authentication succeeded.
- A Recovery Key can be issued and is shown once, for you to write down. Only a verifier for it is
  stored, so after that screen is dismissed the key itself exists nowhere on the device. It can be
  used to reset the Secure Box credential. **If both the credential and the Recovery Key are lost,
  the contents cannot be recovered by anyone, including the developer.**
- Secure Box screens and the Apps Box lock screens block screenshots, screen recording and the
  recents preview while they are open. The alarm screens are not restricted this way.
- Apps Box re-locks whenever the app leaves the foreground. Secure Box does the same by default,
  and you can switch that off in Security settings.

## Alarms, notifications and device permissions

The app requests the following Android permissions, each used only for the alarm or for unlocking:

- **Post notifications** — to show the alarm and its foreground service.
- **Schedule and use exact alarms** — so the alarm rings at the time you set rather than
  approximately.
- **Use full-screen intent** — so the alarm screen can appear when the alarm fires.
- **Vibrate** — when vibration is switched on.
- **Wake lock and foreground service (media playback)** — to keep the alarm ringing reliably.
- **Receive boot completed** — to restore your alarm after a restart, an app update, or a time or
  time-zone change.
- **Use biometric** — for optional biometric unlock.

**The app holds no device administration or device management privileges, and asks for none.**

Two further permissions exist only for the **optional weather section** on the Home screen:

- **Internet** — to ask a public weather service for current conditions.
- **Approximate location** — to know roughly where to ask about. Only the *coarse* permission is
  requested, **never precise location** and **never background location**, so the app cannot read
  your position while it is closed.

The app does **not** request the contacts, microphone or camera permissions.

Two further permissions are added automatically by the Android libraries the app is built on,
rather than requested by AlarmVault itself. They appear in the Google Play permission list, so they
are named here too:

- **View network connections** — added by the media library that powers the Secure Box video
  player. It lets that library check whether a connection exists. AlarmVault plays only files
  already on your device and never streams anything.
- **Use fingerprint** — the older form of the biometric permission, added by the AndroidX biometric
  library so that optional biometric unlock also works on Android 9 and earlier. It covers the same
  unlock as **Use biometric** above, and no fingerprint data ever reaches the app.

When you pick an audio file for the alarm, the app keeps read access to that file so it can still
play it hours later. It stores a reference to the file, not a copy of it.

## Apps Box

Apps Box is a separate protected area with its own lock, independent of Secure Box. It has its own
PIN, password or pattern verifier and its own Recovery Key, stored the same way as Secure Box's.

Apps Box reads the list of installed apps that have a launcher icon so that you can select from it,
and saves the package names of the apps you import. That list is held only on this device. Removing
an app from Apps Box deletes its package name from that list.

### What hiding actually means

You can choose AlarmVault as your device's Home app from Android's own Home settings. AlarmVault
then shows its own home screen and app drawer, and leaves your protected apps out of that drawer.

**That is the entire extent of it.** The apps stay installed, keep running normally, and remain
visible in Android Settings, in search, and in any other launcher you switch to. This is **hiding
from AlarmVault's own home screen — not Android system-level hiding** — and the app does not
describe it as anything more.

One more thing happens when you open a protected app from inside Apps Box: it is started in a way
that keeps it out of the Recents list, so its name and a picture of it are not left on the recent
apps screen for the next person who presses that key. The app itself is untouched and is still
reachable everywhere else described above.

Selecting the Home app is always done in Android's own interface. AlarmVault cannot set or change
the Home app itself, and never attempts to. You can switch your previous home screen back at any
time from the same Android settings, and your protected apps appear there again.

AlarmVault does **not** uninstall another app, does not disable it, does not delete or encrypt its
data, does not read its contents, and does not alter its notifications or settings. Protecting an
app records your choice and leaves it out of one app drawer; nothing else about the device changes.

**AlarmVault holds no device administration or device management privileges, and asks for none.**

To list the apps you can choose from, and to draw its own app drawer, AlarmVault asks Android which
apps have a launcher icon. It uses Android's narrow `<queries>` mechanism for this and does **not**
request the broad "query all packages" permission.

## What the Home screen reads about your apps

When AlarmVault is your Home app it has to know what to draw, so it asks Android for the apps that
have a launcher icon — their names, their icons and their package names. Where a work profile is set
up, that list covers the work profile too, so work apps appear and open normally.

For the fixed row at the bottom of the Home screen, AlarmVault also asks Android which apps you have
set as your default phone, messaging, browser and camera apps, so the row matches your device
instead of assuming a particular brand.

AlarmVault also asks Android which app is currently your home screen, and reads that app's name so
Apps Box can show it to you. That screen states plainly whether AlarmVault is your home app or
another one is, and naming it is what lets you check the answer rather than take it on trust.

To be clear about what that does and does not mean: AlarmVault learns only which app fills each of
those roles. It does **not** read your messages, your calls or your call history, your contacts,
your photos or any account information, and it holds no permission that would let it.

All of this is read on the device, used to draw the screen, and never sent anywhere. Only the
package names you choose to protect in Apps Box, and the shortcuts you remove from Home, are written
down at all.

## Data sharing

The app does not send your data to the developer or to anyone else. It contains **no analytics, no
crash-reporting service, no advertising and no advertising identifier**, and your data is not sold
or shared.

Data leaves the app only when you move it yourself. Exporting an item from Secure Box writes a
decrypted copy to the location you choose. Once exported, that copy is outside the app's protection
and is subject to whatever else can read that location.

The alarm screen also has a **Send feedback** option. It opens your own email app with a message
addressed to the developer and pre-filled with the app version, your Android version and your
phone model, so you do not have to go looking for them. Nothing is sent automatically: the draft
is yours to read, edit or discard, and the app neither sees nor keeps a copy of what you send.

## Internet and network use

The app makes **exactly one kind of network request**: the optional weather section on the
AlarmVault Home screen.

If you have granted approximate location, the Home screen sends an approximate position — rounded
to about a kilometre — to **MET Norway (api.met.no)** to obtain the current temperature and
conditions. That is a free public weather service operated by the Norwegian Meteorological
Institute; no account, API key or sign-in is involved.

**What is sent:** the rounded coordinates, together with the name of the app and the developer's
contact address, which MET Norway require so they can get in touch about a misbehaving caller.
Nothing identifies you: no account, no device or advertising identifier, and nothing about your
alarms, Secure Box, notes or Apps Box list ever leaves the device.

Precise location is never requested, and background location is never requested, so the app cannot
read your position while it is closed. Location is only read while the Home screen is open. The
reading is cached for about an hour so the request is not repeated often, and a failed lookup waits
about twenty minutes before trying again. If you refuse the permission, or the lookup fails, the
Home screen shows the weather as unavailable and works normally.

Weather data is provided by MET Norway under the Creative Commons Attribution 4.0 licence, which is
why the Home screen credits them beneath the reading.

Apart from that one request, the app contains no other networking, server or cloud code. There is no
account, no analytics, no crash-reporting service, no advertising, and no cloud service or hosted
database operated for the app.

## Third-party code included in the app

The app is built on Google's own Android and Jetpack libraries, and on three additional open-source
libraries used purely to read and write archive files on the device. **None of them sends anything
anywhere**; they are file-format code and have no network access of their own.

- **Apache Commons Compress** and **XZ for Java**, under the Apache License 2.0, used to open 7z
  files.
- **junrar**, under the UnRAR licence, used to open RAR files. As that licence requires, it is
  stated here and in the in-app guide that **this code may not be used to develop a RAR (WinRAR)
  compatible archiver**. It can only read RAR files; no app can create them, which is why
  compressing files in Secure Box offers ZIP and 7z but never RAR.

ZIP files are handled by the archive code built into Android itself, with no additional library.

## Data retention and deletion

Your data stays on the device until you remove it:

- Deleting an item from Secure Box deletes its encrypted file and its database record.
- Deleting a note removes it from the database.
- Removing an app from Apps Box removes its package name from the saved list.
- Temporary decrypted copies made for the video and PDF viewers, for video pictures in the list,
  and for extracting or creating an archive, are deleted as soon as they have served their
  purpose, and any left behind are cleared the next time the app starts.
- Deleting an extracted folder is just deleting the items in it; the folder is only the name they
  share and disappears once the last one is gone.
- Adding a shortcut back to Home removes it from the list of shortcuts you had removed.
- The cached weather reading is replaced about an hour after it was fetched.

Uninstalling the app removes its private storage, including the encrypted Secure Box files, the
local database and the preference files. Because the encryption key lives in the Android Keystore
and cannot be exported, encrypted files copied off the device beforehand cannot be decrypted
afterwards. Copies you exported yourself are unaffected by uninstalling.

## Backups and device transfer

Android's backup feature is switched off for this app. In addition, the encrypted vault directory,
the local database and the security preferences are explicitly excluded from cloud backup and from
device-to-device transfer, so Secure Box contents are not copied to another device by those
features.

## Children's privacy

The app has no account system and does not knowingly collect personal information from anyone,
including children. It does not ask for age or identity. The only thing the app itself ever sends
off the device is an approximate location for the optional weather section, and only if you allow
it. The feedback option sends nothing on its own; it opens an email for you to write and send.

## Active development

**AlarmVault is actively under development. As new features are introduced or existing functionality
changes, this Privacy Policy may be reviewed and updated to accurately reflect the app's current
features, permissions, data handling practices, and security behaviour. Users should refer to the
latest version of this Privacy Policy for the current information.**

The copy shown inside the app always ships with that version of the app, so updating the app also
updates the policy you see there. This hosted copy is updated alongside each release.

## Changes to this privacy policy

This policy describes the app as it currently works. As the app changes, this text will be updated
so that it continues to match the app's actual behaviour.

## Contact

For privacy questions, support or feedback about AlarmVault, write to:

**alarmvaultfeedback@gmail.com**

This is also the contact address AlarmVault identifies itself with when it asks MET Norway for the
weather, which that service requires.
