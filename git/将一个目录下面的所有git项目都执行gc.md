```
base_dir=`pwd`
for f in `find -name HEAD`; do 
  cd $base_dir
  cd `dirname $f`; 
  git gc; 
done;
```