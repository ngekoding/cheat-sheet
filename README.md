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
