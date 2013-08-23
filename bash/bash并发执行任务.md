### 类似golang的WaitGroup
```
(sleep 1;echo 1) &
(sleep 1;echo 1) &
(sleep 1;echo 1) &
wait;wait;wait

```

### 通道并发(没试过)
```
find . -iname "*png" -print0 | xargs -0 --max-procs=4 -n 1 pngout
```