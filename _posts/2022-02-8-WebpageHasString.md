# Check in linux if a webpage has a string

```curl -s https://www.whatever.com| grep -q "string"; [ $? -eq 0 ] && echo "yes" || echo "no"```