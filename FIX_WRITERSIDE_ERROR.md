# 修复 Writerside 构建错误指南

## 错误信息
```
Error running "Web Archive (in)"
Couldn't find instance InstanceToBuild(id=, name=Sounean's Algorithm Training Camp, module=, isGroup=false
```

## 已完成的修复
1. ✅ 修复了 `Writerside/cfg/buildprofiles.xml` 的 XML 格式

## 需要在 IDE 中执行的步骤

### 方法 1: 重新加载项目（推荐）
1. 在 Writerside IDE 中，点击 **File** → **Invalidate Caches / Restart**
2. 选择 **Invalidate and Restart**
3. 等待 IDE 重新启动并重新索引项目

### 方法 2: 手动清理缓存
1. 关闭 Writerside IDE
2. 删除项目中的 `.idea` 目录（如果存在 Writerside 相关的缓存）
3. 重新打开项目

### 方法 3: 重新构建项目
1. 在 Writerside IDE 中，点击 **Build** → **Rebuild Project**
2. 或者使用快捷键重新构建

### 方法 4: 检查构建配置
1. 打开 **File** → **Settings** → **Build, Execution, Deployment** → **Writerside**
2. 确认实例配置正确指向 `in` 实例
3. 如果配置不正确，重新配置并保存

## 验证修复
构建完成后，检查是否还有错误。如果问题仍然存在，请尝试：
- 检查 `Writerside/in.tree` 文件是否有语法错误
- 确认所有引用的 topic 文件都存在
- 查看 Writerside 的日志文件以获取更详细的错误信息

