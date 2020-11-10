# cheat-sheet
## GIT (Version Control)
##### Baru bikin
```
- echo "# sistem-upload" >> README.md
- git init
- git add README.md
- git commit -m "first commit"
- git remote add origin https://github.com/ngekoding/sistem-upload.git
- git push -u origin master
```
##### Mengatur Username & Email
```
- git config --global user.name "Nur Muhammad"
- git config --global user.email "blog.nurmuhammad@gmail.com"
* Cara diatas untuk mengatur disemua repositori, untuk spesifik hilangkan "--global"
```
##### PUSH
```
- git add .
- git commit -m "Your messages"
- git push -u origin master --> master is your "branch"
```
##### PULL
```
- git pull origin master
```
##### REMOVE
```
git rm file --> file is your file name
            --> and then, use PUSH
```
##### SHOW CONFIG
```
git config --list
```
##### REMOVE A COMMIT THAT ALREADY PUSHED
1. `git log` to find out the commit you want to revert
2. `git push origin +7f6d03:master` while `7f6d03` is the commit before the wrongly pushed commit. + was for force push

## PHP (How to do something?)
##### Remove HTML Tag from string
```
$content = strip_tags($content);
```
##### Get first image from string
```
preg_match('/<img.+src=[\'"](?P<src>.+?)[\'"].*>/i', $content, $image);
echo $image['src'];
```
##### Remove img tag from string
```
preg_replace("/<img[^>]+\>/i", "(image) ", $content);
echo $content;
```
##### Checking valid URL
```
public function valid_url($url) {
    if (!preg_match( '/^(http|https):\\/\\/[a-z0-9_]+([\\-\\.]{1}[a-z_0-9]+)*\\.[_a-z]{2,5}'.'((:[0-9]{1,5})?\\/.*)?$/i', $url)) {
        return FALSE;
    }
    return TRUE;
}
```

## CSS Tricks
#### CSS Triangle
```
.arrow-up {
  width: 0; 
  height: 0; 
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-bottom: 5px solid black;
}

.arrow-down {
  width: 0; 
  height: 0; 
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
  border-top: 20px solid #f00;
}

.arrow-right {
  width: 0; 
  height: 0; 
  border-top: 60px solid transparent;
  border-bottom: 60px solid transparent;
  border-left: 60px solid green;
}

.arrow-left {
  width: 0; 
  height: 0; 
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent; 
  border-right:10px solid blue; 
}
```
