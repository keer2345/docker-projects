# docker-projects
- [10 best practices to containerize Node.js web applications with Docker](https://snyk.io/blog/10-best-practices-to-containerize-nodejs-web-applications-with-docker/)
- [Top 8 Docker Best Practices for using Docker in Production](https://dev.to/techworld_with_nana/top-8-docker-best-practices-for-using-docker-in-production-1m39)
- [6 Docker Compose Best Practices for Dev and Prod](https://releasehub.com/blog/6-docker-compose-best-practices-for-dev-and-prod)
- [10 Docker Security Best Practices](https://snyk.io/blog/10-docker-image-security-best-practices/)


# Configure
`cat  /etc/docker/daemon.json`
```json
{
    "registry-mirrors": ["https://docker.registry.cyou",
    "https://docker-cf.registry.cyou",
    "https://dockercf.jsdelivr.fyi",
    "https://docker.jsdelivr.fyi",
    "https://dockertest.jsdelivr.fyi",
    "https://mirror.aliyuncs.com",
    "https://dockerproxy.com",
    "https://mirror.baidubce.com",
    "https://docker.m.daocloud.io",
    "https://docker.nju.edu.cn",
    "https://docker.mirrors.sjtug.sjtu.edu.cn",
    "https://docker.mirrors.ustc.edu.cn",
    "https://mirror.iscas.ac.cn",
    "https://docker.rainbond.cc"]
}
```
