Option 1 — localhost.run (Easiest, No Install Needed)
Open Git Bash on the VM and run:


ssh -R 80:localhost:80 nokey@localhost.run
It will give you a public URL like:


https://abc123def.lhr.life
Anyone on the internet can open that URL and access your app. Share it with your team to test.

To stop: Press Ctrl+C in Git Bash.
