# sDDF Beginner Guide
Getting started guide for the first time building the sDDF


1. Clone the sel4cp and switch to the "benchmark" branch: 
```
git@github.com:lucypa/sel4cp.git
```
  
2. Clone the sDDF repo:
```
https://github.com/lucypa/sDDF
```

3. Clone the specific seL4 repo:
```
git@github.com:BreakawayConsulting/seL4.git
```
  - Switch to the ```sel4cp-core-support``` branch.

  - Checkout the ```92f0f3ab28f00c97851512216c855f4180534a60 ``` commit 

  - If building for the imx8mm, run the following commands:
  ```
  rm seL4/libsel4/sel4_plat_include/imx8mm-evk
  cp -r seL4/libsel4/sel4_plat_include/imx8mq-evk seL4/libsel4/sel4_plat_include/imx8mm-evk
  ```


4. Get all the dependencies outlined in the sel4cp Readme.
You may potentially have to build musl from scratch if your version does not work:
```
https://git.musl-libc.org/cgit/musl/tag/?h=v1.2.2
https://git.musl-libc.org/cgit/musl/tree/INSTALL
```
  - And then make sure to add ```/usr/local/musl/bin``` to your path, as well as ensuring the sel4cp arm toolchain is in the path. 

5. Get all the dependencies as per the following resource:
```
https://docs.sel4.systems/projects/buildsystem/host-dependencies.html
```
6. Build the sel4cp according to the instructions in the sel4cp Readme.

  - If an error occurs relating to building documentation, in the build_sdk.py file, comment out line 360, which is the call to build_doc.

7. Get the ```libc.a``` file in this repo.

8. In the ```sDDF/echo_server``` create a directory called ```lib``` and place the ```libc.a``` file in there.

9. In the ```sDDF/echo_server/Makefile``` add the following line to the LDFLAGS: 
```
-L$(BOARD_DIR)/lib -Llib
````
