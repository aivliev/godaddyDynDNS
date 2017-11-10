For now is just copypaste of 
https://ru.godaddy.com/community/Managing-Domains/Dynamic-DNS-Updates/m-p/60614#M15277



Before adding the cronjob, I put the script in /usr/local/bin, chowned it to nobody and chmoded it to 700. This was to prevent other users reading the script (to find the key and secret) or executing it (to update the records).
 
I then ran touch /var/log/updatedomain.log and chowned it to nobody.
 
Finally I edited nobody's crontab using crontab -e -u nobody and set it up as follows:
#
SHELL=/bin/sh
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/pkg/bin
HOME=/var/tmp
CRON_WITHIN=240
#
#minute hour    mday    month   wday    command
#
*/15    *       *       *       *       /usr/local/bin/updatedomain www mydomain.com >> /var/log/updatedomain.log
You can, of course, substitute www for @ to update the actual domain's A record and add more lines to the crontab to update the A records of various different domains.
 
I hope this helps somebody. Smiley Very Happy
