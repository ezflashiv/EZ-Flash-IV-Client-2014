# Flushing the `postfix` queue

```
cd /var/spool/postfix/active
find . | xargs grep -l "WHATEVER THE MAILS SUBJECT IS" | awk '{print "rm -f "$1}' > doit.sh
# review the doit.sh, make sure it's OK
. doit.sh
```