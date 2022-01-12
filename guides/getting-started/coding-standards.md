# Coding Standards

## **Update on Jan 2022:**

FLY, update lại `indentation rules` theo chuẩn quốc tế đang dùng ([https://github.com/airbnb/javascript#whitespace](https://github.com/airbnb/javascript#whitespace)) là 2 spaces.\
Cách update như sau:\
Với ae dùng VSCode thì cần cài 2 extensions: EditorConfig và ESLint, sau khi cài xong thì expect là VSCode sẽ follow theo configs ở file `.editorconfig` trong project luôn, trong trường hợp ko thấy apply thì cần kiểm tra lại xem có đang bật extension format nào khác ko.\
Với ae dùng Webstorm thì cũng cần cài plugin Editorconfig và bật eslint trong phần Languages & Framework lên là đc.\
Hiện tại với project `pfcore` thì sẽ chưa bắt buộc phải format lại code, cần update dần dần, để tránh việc format toàn bộ file, mọi người có thể sử dụng cách sau:\
Khi đang edit 1 file trong webstorm, dùng tổ hợp `CMD+Option+Shift+L`, sẽ hiện lên bàng lựa chọn format option, chọn vào `Only VCS changed code`.\
Ngoài ra nếu muốn format toàn bộ file với eslint thì có thể cài phím tắt ở webstorm như sau: Vào Preferences => tìm `fix eslint problems` => gán phím tắt.\
Sau đó quay lại file edit và sử dụng phím tắt vừa tạo để format.![](broken-reference)

![CMD+Option+Shift+L](<../../.gitbook/assets/Screen Shot 2022-01-10 at 15.33.20.png>)

![Add eslint fix hotkey](<../../.gitbook/assets/Screen Shot 2022-01-10 at 15.39.40.png>)

## **Coding Styles**

ESLint with `react-app` rules

**Rule #1: Always define your function/component type**

And put it into `src/types` folder

**Rule #2: Always format your code before committing.**

This project is using pre-commit hooks to check if your code is valid and formatted or not, otherwise you cannot commit and push your code to the repository. So please make sure that your code is formatted and linted using ESlint before you commit.

**Tips:** If you use Webstorm, please navigate to `Preferences` => `ESLint` and enable the ESLint. After that, go to `Keymap` and search for `Fix Eslint problems` and assign a shortcut to use.

**Rule #3: Commenting your code**

Please read this article to see how to documenting your code: https://react-styleguidist.js.org/docs/documenting.html

**Rule #4: Write test for your code**

Resource: https://jestjs.io/docs/en/getting-started.html

**Rule #5: Separation of Concerns**

* Do not write Logic, UI view, Data in one single file, we have to separate it into Components/Custom Hooks/ Stores,...
* Limiting usage of state-full component since it storing data and View in one file. The better way to do it is using hook & custom hook.
* Each code file should not contain more than 300 line of code, we should break it down to a smaller file.
