We navigate to their website first and under the _Our Services_ section, we find a link to a GitHub repository. The `auth-server.c` file seems to be a normal "authentication server" implementation which looks secure, at least on first sight. We also note that there have been 3 commits. If we look at the diff between the latest two commits, we see the following in the ```auth-server.c```'s diff:
```
    // Sample Account
    // Username: walter.parker
    // Password: gh05t_1n_4_5h311c0d3
```

If we look at the _Contacts_ section on the wesbite, we find the email id's of the leadership team: _jane.morningstar@deltaegrep.com_ and _walter.parker@deltaegrep.com_. Furthermore, on the _Insights_ section of the website, note the reference to Cyber Security Community IITB. Doing a quick Google search gives us their website: https://cseciitb.github.io/

We try logging into their mail server with the email id _walter.parker@deltaegrep.com_ and password as _gh05t_1n_4_5h311c0d3_. We succeed! We notice three mails, two of them from Jane Morningstar. We notice an article at https://trustlab.iitb.ac.in/trust-matters-2024-apr-hsbc-tl-ctf and Jane stating that the picture of the CTF challenge setters was taken from his phone. Another mail tells us about the password.

For the first part, we scan the CSeC website and try to find members who are interested in cryptography and look at their socials and webistes. We find Nilabha Saha to be interested in it and a link to his website at https://www.cse.iitb.ac.in/~nilabhasaha/. If we naviagte to the Projects section, we see a report on Pairing-Based Cryptography. We open the report and jump to the implementations section to notice that he used the `pbc` library. A quick Google search leads us to https://crypto.stanford.edu/pbc/ and we note that the author of the library is **Ben Lynn**.

For the second part, we navigate to the webiste to find the _Setting the Challenges_ section with a picture of the CTF challenge makers. We download the image and look at the EXIF data associated with the image (for instance, using `exiftool` on the image). This leads us to find out that the camera model name being **Galaxy S24 Ultra**.

With these, we now log into their mail server again with the email id _jane.morningstar@deltaegrep.com_ and password as _benlynn-galaxys24ultra_. We find two mails, the second one giving us the flag: `HSBC{051nt_y0ur_w4y_2_gl0ry}`