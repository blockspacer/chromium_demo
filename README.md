# Demo

这个项目用来演示如何使用 chromium 中的一些基础机制，包括异步多任务，mojo，多进程等。

> 提示：如果你是 chromium 的新手，建议按照顺序学习这些 demo。

Demo 列表：

1. `demo_exe`: 最简单的 demo，演示 gn 及创建自己的 exe；
2. `demo_log`: 演示使用日志库；
3. `demo_tracing_console`: 演示使用 Trace 输出到控制台；
6. `demo_tasks`: 演示使用线程池 ThreadPool;
7. `demo_messageloop`: 演示使用消息循环 MessageLoop;
8. `demo_mojo_single_process`: 演示在单进程中使用 `mojo` 库；
9. `demo_mojo_multiple_process`: 演示在多进程中使用 `mojo` 库；
10. `demo_mojo_multiple_process_binding`: 演示在多进程中使用 `mojo` 库的 binding 层；
11. `demo_services`: 演示使用基于 `mojo` 的 servcies 及多进程架构；
12. `demo_ipc`: 演示使用基于 `mojo` 的 IPC 接口；
13. `demo_memory`: 演示使用 SharedMemory；
14. `demo_tracing_perfetto`: 演示将 Trace 输出为 Json 格式（用来对接 perfetto）；
15. `demo_tracing_perfetto_content`: 演示 content 模块是如何对接 perfetto 的；
16. `demo_resources`: 演示 resources 相关内容，包括 grit，l10n，pak 等；
17. `demo_viz_gui`: 演示使用 `viz` 显示 GUI 界面；
18. `demo_viz_offscreen`: 演示使用 `viz` 进行离屏渲染；
19. `demo_cc_gui`: 演示使用 `cc` 显示 GUI 界面；
20. `demo_cc_offscreen`: 演示使用 `cc` 进行离屏渲染；
21. `demo_views`: 演示使用 `//ui/views` 创建 UI；
22. `demo_apk`: 演示创建 Android 应用，base::android::* 和 JNI 的使用；
23. `demo_shell`: 演示使用 content api, 创建一个精简的浏览器，支持 Linux 和 Android；

文档列表：

1. [Mojo](./docs/mojo.md)
1. [浏览器启动流程简述](./docs/startup.md)

公共文档在 [docs](./docs) 目录，其他文档在代码相应目录下。

## 用法一（推荐）

1. 进入 chromium 的 `src` 目录；
2. 执行以下命令将该仓库 clone 到 `src/demo` 目录下；

    ```sh
    git clone git@gitlab.gz.cvte.cn:CrOS/seewo/demo.git demo
    ```

3. 找到你的编译输出目录中的 `out/Default/args.gn` 文件，添加以下参数：

    ```python
    # add extra deps to gn root
    root_extra_deps = ["//demo"]
    ```

4. 执行 `ninja -C out/Default demo` 生成所有 demo 程序（详见 [BUILD.gn](./BUILD.gn)）；

## 用法二（使用 gclient)

1. 进入 chromium 项目的根目录（src 上一层目录）找到 `.gclient` 文件；
2. 打开 `.gclient` 文件，参照下面的设置进行修改：

    ```python
    solutions = [
        { "name"        : "src",
            "url"         : "git@gitlab.gz.cvte.cn:CrOS/src.git",
            "deps_file"   : "DEPS",
            "managed"     : False,
            "custom_deps" : {
                # let gclient pull demo project to 'src/demo' dir
                "src/demo": "git@gitlab.gz.cvte.cn:CrOS/seewo/demo.git",
            },
            "custom_vars": {},
        }
    ]
    ...
    ```

3. 找到你的编译输出目录中的 `out/Default/args.gn` 文件，添加以下参数：

    ```python
    # add extra deps to gn root
    root_extra_deps = ["//demo"]
    ```

4. 执行 `gclient sync` 同步代码，这会拉取 `demo` 仓库到 `src/demo` ；
5. 执行 `ninja -C out/Default demo` 生成所有 demo 程序（详见 [BUILD.gn](./BUILD.gn)）；

## TODO

- 完善进程初始化部分的文档 ([docs/startup.md](docs/startup.md))；
- 完善 UI 部分的文档 ([docs/ui.md](docs/ui.md))；
- 完善 content 模块的文档 ([docs/content.md](docs/content.md))；
- 完善 demo_shell 的文档 ([demo_shell/README.md](demo_shell/README.md))；
- 添加 demo, 演示如何创建 aar 组件；
- 添加 demo, 演示如何向 Blink 注入新的 JS 对象；
- 添加 demo, 演示如何实现网页的离屏渲染；
- 添加 demo, 演示如何使用 aura 创建 UI 界面；
- 添加 demo, 演示如何使用 PlatformWindow 创建窗口；

## 更新日志

### 2020.5.21

- 添加 demo_tracing_perfetto_content, 演示 content 模块是如何将 trace 保存到文件的，该文件可以用于 chrome://tracing；
- 添加 demo_tracing 的文档 [demo_tracing](./demo_tracing/README.md)；

### 2020.5.18

- 将 demo_tracing 移动到 demo_tracing 文件夹，并改名为 demo_tracing_console, 添加 Flush 功能；
- 添加 demo_tracing_perfetto, 演示 trace 和 perfetto 的集成及使用；

### 2020.4.29

- 添加 demo_cc_gui， 演示使用 `cc` 显示 GUI 界面；

### 2020.4.17

- 添加 demo_cc 的 TRACE.txt, 用于协助理解 cc 的运行时行为；

### 2020.4.10

- 添加 demo_cc_offscreen, 演示使用 `cc` 进行离屏渲染；

### 2020.4.6

- 添加 demo_viz_offscreen, 演示使用 `viz` 进行离屏渲染；
- 修改 demo_viz 为 demo_viz_gui，功能不变；

### 2020.3.31

- 添加 demo_viz, 演示使用 `viz` 模块；
- 添加 `viz` 的文档：[viz](./demo_viz/README.md)

### 2020.3.21

- 添加 demo_views，演示使用 `//ui/views` 开发 UI;  

### 2020.3.12

- demo_apk 支持 JNI 调用 C++类的实例方法；
- 添加文档：[浏览器启动流程简述](./docs/startup.md)

### 2020.3.7

- demo_apk 支持 JNI；
- 添加文档： [demo_apk](./demo_android/README.md)

### 2020.3.4

- 添加 demo_tracing，用来演示 trace 的使用；
- 添加 demo_apk，用来演示如何使用 gn 创建 Android 应用；
- 添加 demo_shell，用来演示如何使用 Content API 创建一个精简浏览器；

### 更早

添加以下 demo 及相关文档：

- demo_exe: 最简单的 demo，演示 gn 及创建自己的 exe；
- demo_log: 演示使用日志库；
- demo_tracing: 演示使用 Trace；
- demo_tasks: 演示使用线程池 ThreadPool;
- demo_messageloop: 演示使用消息循环 MessageLoop;
- demo_mojo_single_process: 演示在单进程中使用 mojo 库；
- demo_mojo_multiple_process: 演示在多进程中使用 mojo 库；
- demo_mojo_multiple_process_binding: 演示在多进程中使用 mojo 库的 binding 层；
- demo_services: 演示使用基于 mojo 的 servcies 及多进程架构；
- demo_ipc: 演示使用基于 mojo 的 IPC 接口；
- demo_memory: 演示使用 SharedMemory；
