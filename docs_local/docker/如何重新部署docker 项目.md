根据你的项目配置，这是一个包含MySQL、Redis和Next.js应用的完整Docker项目。以下是重新部署的步骤：

快速重新部署
完整重新部署（推荐）：


docker-compose down && docker-compose up -d --build
分步操作
1. 停止并删除现有容器：


docker-compose down
2. 重新构建并启动（如果代码有更新）：


docker-compose up -d --build
3. 仅重启（代码无更新）：


docker-compose up -d
查看状态
查看运行状态：


docker-compose ps
查看日志：


# 查看所有服务日志
docker-compose logs -f

# 查看特定服务日志
docker-compose logs -f app
清理重建（彻底重置）
如果需要完全清理并重新开始：


# 停止并删除容器、网络、卷
docker-compose down -v

# 重新构建并启动
docker-compose up -d --build
⚠️ 注意：-v 参数会删除数据卷，包括MySQL和Redis的数据。