### 将远程项目镜像到本地 pull镜像
```
git fetch origin --mirror
git fetch origin +refs/heads/*:refs/heads/*
```

### 将本地项目镜像到远程 push镜像
```
git push origin --mirror
```

```
git push origin refs/heads/*:refs/heads/*
```

### 将远程某项目镜像到本地的裸项目
```
mkdir ./monster
cd ./monster
git init --bare
git remote add origin git@10.1.1.6:/git/monster
git fetch origin +refs/heads/*:refs/heads/*
```