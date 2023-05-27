# simple-signage
Simple Signage Player (Designed for Raspberry Pi)

This is another one of these projects that I've put here mainly so I don't lose it as I've rewritten it once already.

It's designed as a really lightweight digital signage player for a raspberry pi that was designed to allow simple static signage to be updated without any technical skills by practically anyone. 

### Installation (Pi) 

More detailed installation instructions will follow but for simplicity I'd recommend using DietPi in Kiosk Mode (or whatever your preferred pi standalone web kiosk method is) and set the URL to http://localhost/ 

Simply copy the contents of this repository to `/var/www/html` on the pi, ensuring that the directory /var/www/html/assets is writeable (chmod 777) by whoever needs to upload signage images or change the programme of displayed signage. To simplify this I used `rclone` to sync from Dropbox periodically in cron;

```rclone sync dropbox:/signage /var/www/html/assets```

### Updating the Signage

Simply place PNG files 1920x1080 in the assets directory by whatever means and configure the `display.txt` file to include them. The format of this file is a simple CSV as follows;

```
1,welcome.png,3,0000,1900
1,bar_prices.png,3,1900,2200
1,goodnight.png,7,2200,2359
1,coming_up_1.png,7,2200,2359
1,coming_up_2.png,7,2200,2359
1,coming_up_3.png,7,2200,2359
```

The first column is unused in this release. The second parameter is the file name, the next parameter is how long to display it for before preceding to the next slide, and the two parameters on the end are the time that this is to be shown. 

The above example shows the "Welcome" screen all day until the bar opens at 1900. The bar prices from 1900-2200. Then a "Thank you and goodnight" message and slideshow after the bar closes.

### Simple Design

This is a single page HTML/JS file that was made as simple as possible. It relies on the excellent https://github.com/mholt/PapaParse library to parse the CSV out of laziness but has no other external dependencies (e.g on things like jQuery) and does not require an internet connection to operate.
