TRYHACKME WEB CHALLANGE - MD2PDF (Writeup)


In this challenge, the goal was to find the flag by testing a web application that converts Markdown to PDF.

First, I started the machine and opened the website using the given IP address. The application allowed me to enter text and convert it into a PDF file.

At the beginning, I tried some basic payloads to read local files, but they did not work and returned errors. This showed that some inputs were filtered.

After that, I used  to find hidden paths in the web application. This helped me understand that there might be additional functionality running in the background.

Then I focused again on the Markdown to PDF feature. I realized that the application renders HTML inside the PDF. So I tried injecting HTML code.

I used the following payload:

<iframe src="http://localhost:5000/admin"></iframe>

This worked because the server processed the request internally. The PDF generator loaded the admin page from localhost and included it in the PDF.

When I opened the generated PDF, I could see the admin page content, and the flag was visible there.



What I learned

- Web applications can be vulnerable when they render user input without proper filtering
- Markdown to PDF tools can be abused using HTML injection
- Internal services (localhost) can sometimes be accessed using SSRF-like techniques
- is useful for discovering hidden paths



Tools Used

- Browser (to interact with the web app)
- (for directory discovery)



Conclusion

This challenge showed how a simple feature like PDF generation can be exploited to access internal resources and retrieve sensitive data like flags.
