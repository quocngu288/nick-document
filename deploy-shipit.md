# Shipit – Tự động deploy Javascript project

## Shipit là gì?

Shipit là công cụ tự động hoá các bước deploy dành cho các bạn Javascript developer. 1 dòng lệnh trong Shipit config ta coi như 1 task. Shipit sẽ thực hiện 1 flow tasks dựa trên package orchestrator, login và chạy các lệnh SSH trên server thông qua OpenSSH. Chúng ta có thể sử dụng Shipit để tự động hoá build và deploy cho hàng loạt các ứng dụng Nodejs.

## Shipit là gì?

Shipit là công cụ tự động hoá các bước deploy dành cho các bạn Javascript developer. 1 dòng lệnh trong Shipit config ta coi như 1 task. Shipit sẽ thực hiện 1 flow tasks dựa trên package orchestrator, login và chạy các lệnh SSH trên server thông qua OpenSSH. Chúng ta có thể sử dụng Shipit để tự động hoá build và deploy cho hàng loạt các ứng dụng

### Chuẩn bị:

- Server chạy Ubuntu hoặc Debian Linux và cài đặt rsync.

- Web server Apache.
- node và yarn được cài đặt trên môi trường development. Ở máy tôi đang cài Nodejs 14.19.0 và yarn 1.22.17 trên Ubuntu 21, npm cũng được.

### Bước 1: Khởi tạo git repo

```json
https://github.com/quocngu/vuejs-demo.git
```

### Bước 2: Cài đặt Shipit package

Tạo 1 file package.json:

```json
yarn init
```

Cài đặt Shipit

```json
yarn add --dev shipit-cli
yarn add --dev shipit-deploy
```

### Bước 3: Config shipit

Có thể copy file này, sau đó sửa các config information cho phù hợp với project của mình.

```js
module.exports = (shipit) => {
  require("shipit-deploy")(shipit);

  const stagingConfig = {
    deployUser: "bitnami",
    key: "doc/aws/server-staging.pem",
    deployTo: "/home/bitnami/htdocs/projects/",
  };

  // More default config goes here

  shipit.initConfig({
    staging: {
      ...stagingConfig,
      projectName: "angular-demo",
      servers: ["bitnami@xxx.xxx.xxx.xxx"],
    },
  });
};
```

- stagingConfig: gom các config nào giống nhau ở các môi trường lại, mục đích cho gọn gàng và dễ import và chỉnh sửa khi cần.

- staging: alias của server mà dùng để deploy project của mình lên. Các server alias thường sử dụng như production, development,…

- projectName: định danh tên của project, chỗ này sẽ dùng để xác định thư mục deploy.

- key: trong trường hợp này folder ./doc/aws/ để chứa các server key. Nhớ thêm vào git ignore của mình.

Sau đó tôi viết thêm task cần thiết cho việc deploy như build project, setup remote server,…

```js
...
shipit.task("vuejs:deploy", async () => {
    let zipFileName = `${shipit.config.projectName}.zip`

    // Zip the dist folder into dist.zip package then remove the folder as we don't need it anymore
    await shipit.local(`cd dist && zip -r ../${zipFileName} ${shipit.config.projectName}`);

    // Create deployTo folder if it's not existed
    await shipit.remote(
      `sudo mkdir -p ${shipit.config.deployTo} && sudo chown -R ${shipit.config.deployUser}: ${shipit.config.deployTo}`
    );

    // // Copy dist.zip to servers
    await shipit.copyToRemote(zipFileName, shipit.config.deployTo);

    // // Remove the dist.zip
    await shipit.local(`rm ${zipFileName}`);

    // // remove old frontend files
    await shipit.remote(`rm -rf ${shipit.config.deployTo}/${shipit.config.projectName}/*`);

    // // On server, unzip the dist.zip file then remove the zip package
    await shipit.remote(
      `cd ${shipit.config.deployTo} && unzip -o ${zipFileName} && rm ${zipFileName}`
    );
  });
```

Cần lưu ý:

- vuejs:deploy: đặt tên cho task mà sẽ gọi lúc deploy.
- Các task khác đã để comment vào rồi

Cuối cùng ta được file config như sau:

```js
module.exports = function (shipit) {
  // Load shipit-deploy tasks
  require("shipit-deploy")(shipit);

  const stagingConfig = {
    deployUser: "bitnami",
    key: "doc/aws/server-staging.pem",
    deployTo: "/home/bitnami/htdocs/projects/",
  };

  shipit.initConfig({
    staging: {
      ...stagingConfig,
      projectName: "angular-demo",
      servers: ["bitnami@xxx.xxx.xxx.xxx"],
    },
  });

  shipit.task("angular:deploy", async () => {
    let zipFileName = `${shipit.config.projectName}.zip`;

    // Zip the dist folder into dist.zip package then remove the folder as we don't need it anymore
    await shipit.local(
      `cd dist && zip -r ../${zipFileName} ${shipit.config.projectName}`
    );

    // Create deployTo folder if it's not existed
    await shipit.remote(
      `sudo mkdir -p ${shipit.config.deployTo} && sudo chown -R ${shipit.config.deployUser}: ${shipit.config.deployTo}`
    );

    // // Copy dist.zip to servers
    await shipit.copyToRemote(zipFileName, shipit.config.deployTo);

    // // Remove the dist.zip
    await shipit.local(`rm ${zipFileName}`);

    // // remove old frontend files
    await shipit.remote(
      `rm -rf ${shipit.config.deployTo}/${shipit.config.projectName}/*`
    );

    // // On server, unzip the dist.zip file then remove the zip package
    await shipit.remote(
      `cd ${shipit.config.deployTo} && unzip -o ${zipFileName} && rm ${zipFileName}`
    );
  });
};
```

Đến đây về cơ bản đã hoàn thành xong việc setup shipit. Có thể deploy project lên môi trường staging bằng command sau:

```json
./node_modules/.bin/shipit staging angular:deploy
```

Đặt trường hợp muốn chạy thêm command gì đó ví dụ build application trước khi deploy, chạy câu sau:

```json
ng build angular --prod --aot && ./node_modules/.bin/shipit staging angular:deploy
```

Quá dài, để ghi nhớ và gõ . Làm thêm 1 bước là gom các command cần thiết vào cùng 1 file, sau này chỉ cần execute file này khi muốn deploy, chỉnh sửa hay thêm bớt command cũng dễ dàng.

```json
#!/usr/bin/env bash
ng build angular --prod --aot && ./node_modules/.bin/shipit staging angular:deploy
```

Sau này bất cứ khi nào cần deploy staging chỉ cần chạy command:

```json
deploy/angular-demo-staging.sh
```
