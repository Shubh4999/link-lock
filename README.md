# Link Lock

[Password-protect URLs using AES in the
browser.](https://link-lock.theanimecentreindia.tech)

Link Lock now supports secure, hidden bookmarks via bookmark knocking!



## About

Link Lock is a tool for encrypting and decrypting URLs. When a user visits an
encrypted URL, they will be prompted for a password. If the password is
correct, Link Lock retrieves the original URL and then redirects there.
Otherwise, an error is displayed. Users can also add hints to display near the
password prompt.

Each encrypted URL is stored entirely within the link generated by the
application. As a result, users control all the data they create with Link
Lock. Nothing is ever stored on a server, and there are no cookies, tracking,
or signups.

Link Lock has many uses:

- Store private bookmarks on a shared computer
- Encrypt entire web pages
- Send sensitive links over public or insecure channels (e.g., posting links
  to a public website that require a password to access)
- Implement simple CAPTCHAs – particularly effective against basic web scrapers
  that do not respect `robots.txt`
- Add a password to shared Dropbox or Google Drive links
- Share password-protected magnet links and torrents
- [Evade censorship](#evading-censorship)

Link Lock uses AES in GCM mode to securely encrypt passwords, and PBKDF2 and
salted SHA-256 (100,000 iterations) for secure key derivation. Encryption,
decryption, and key derivation are all performed by the [`SubtleCrypto`
API](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto). The
initialization vector is randomized by default, but the salt is not.
Randomization of both the initialization vector and salt can be enabled or
disabled by the user via "advanced options." The salt and initialization vector
are sent with the encrypted data if they are randomly generated. The API is
versioned such that old encrypted links will always work, even if later
versions of Link Lock are updated to be more secure. Please read the code
([`api.js`](https://github.com/Shubh4999/link-lock/blob/master/api.js) in
particular) for more information.


## Examples

- [Regular link encryption](Url) - Password: GG1@
- [Emoji
  support](url) - Password: avocado
- [Share
  torrents](Url) - Password: torrenting_is-legal!



## Disclaimer

The code was written to be read. Please read it, especially if you don't trust
me to build a secure encryption application. In particular:

- ~~I am a college student, not a security professional – there may be best
  practices I am not aware of.~~ I have graduated college, and now work for a
  cybersecurity company. 
- Once someone decrypts a link, they can share the original URL as much as they
  want. Only share encrypted links with trusted people.
- I am not comfortable using JavaScript, and I don't have a firm grasp of the
  nuances of the language – there may be bugs that I don't even know to check
  for.
- This is the first project I have ever done using encryption – there is likely
  a subtle mistake somewhere.
- Most of the encryption/decryption code is based on [MDN
  tutorials](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/deriveKey#PBKDF2_2)
  for the `SubtleCrypto` API.



## Usage

- Create a locked link here: [https://link-lock.theanimecentreindia.tech](https://link-lock.theanimecentreindia.tech).
- Once you have a locked link, create a hidden bookmark here:
  <https://link-lock.theanimecentreindia.tech/hidden>.
- Use the advanced options when creating a link to make the encryption more
  secure (at the cost of a longer link).
    - By default, the initialization vector is randomized for security, but
      this can be disabled, even though doing so is a vulnerability.
    - By default, the salt used to hash the password during key derivation is
      not randomized, but this can be enabled.
- To bookmark a locked link, drag it from the output box to the bookmarks bar.
  Alternatively, visit the locked link and bookmark it before entering the
  password.
- If you lose the password, it is almost impossible to recover the original
  link. The strong security guaranteed by encryption can be a blessing or a
  curse if you are not careful!
- Currently, the only way to recover a lost password is by trying all possible
  options (very slowly) by brute force. An example application to brute force
  Link Lock URLs in the browser can be found here:
  <https://link-lock.theanimecentreindia.tech/bruteforce>.
- A parallelized, cross-platform, CPU-based brute forcer can be found here:
  <https://github.com/Shubh4999/bruteforce-link-lock>
- If you receive a Link Lock URL that you do not trust, decrypt it using this
  interface that does not automatically redirect:
  <https://link-lock.theanimecentreindia.tech/link-lock/decrypt>.

### Evading Censorship

Link Lock can be used to evade censorship. If you are concerned that sending
links with the `jstrieb.github.io` domain name will put you at risk, just
replace the domain with another. For example, share

```
https://wikipedia.org/#eyJ2IjoiMC4wLjEiLCJlIjoicmZVOWNIZ3l6ZDJCQklyVEF6bS8rNnUxM2xGQ3UxN2wrYWVNM25QOC9nNlRJU3pnc21YUlFMQVJ0QjMrczNERG8yWFN2RXdZNUhkeEdhWTJyNmljTnpNWVNoYkdwV0xtMnVMQ3pHNVAiLCJoIjoiMSArIDEgPSA/IiwicyI6IkRxQW1iRnQ2ZUJWU2UxcjRFeXVlTkE9PSIsImkiOiJGQjA0QU5yUURvbjI0UEw5In0=
```

instead of

```
https://link-lock.theanimecentreindia.tech/#eyJ2IjoiMC4wLjEiLCJlIjoicmZVOWNIZ3l6ZDJCQklyVEF6bS8rNnUxM2xGQ3UxN2wrYWVNM25QOC9nNlRJU3pnc21YUlFMQVJ0QjMrczNERG8yWFN2RXdZNUhkeEdhWTJyNmljTnpNWVNoYkdwV0xtMnVMQ3pHNVAiLCJoIjoiMSArIDEgPSA/IiwicyI6IkRxQW1iRnQ2ZUJWU2UxcjRFeXVlTkE9PSIsImkiOiJGQjA0QU5yUURvbjI0UEw5In0=
```

Any domain can be used in place of `wikipedia.org`. That way, a malicious
third-party who clicks the altered link will be taken to a valid page, which
helps alleviate suspicion. When sharing the password to unlock the link,
explain how to switch out the domain name with either
`link-lock.theanimecentreindia.tech`, or with the path to a local clone of Link Lock.
Using a local copy is particularly recommended for evading censorship, since no
request to my domain is ever made.
## Project Status

This project is actively maintained. If there are no recent commits, it means
that everything has been running smoothly! Even if the link storage protocol
is updated, Link Lock is designed to be 100% backwards-compatible, so your
locked links will never break.



# Support the Project

There are a few things you can do to support the project:

- Star the repository and follow me on GitHub
- Share and upvote on sites like Twitter, Reddit.
- Report any bugs, glitches, or errors that you find
- Translate into other languages

These things motivate me to to keep sharing what I build, and they provide
validation that my work is appreciated! They also help me improve the project.
Thanks in advance!

If you are insistent on spending money to show your support, I encourage you to
instead make a generous donation to one of the following organizations. By
advocating for Internet freedoms, organizations like these help me to feel
comfortable releasing work publicly on the Web.
