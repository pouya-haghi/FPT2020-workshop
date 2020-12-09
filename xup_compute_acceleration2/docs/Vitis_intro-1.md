---
layout: default
---

# Introduction to Vitis Part 1

## Introduction

This lab guides you through the steps involved in creating a Vitis project using Graphical User Interface (GUI). After creating the project, you will run software emulation to verify functionality of the design.

Check [Creating a Vitis IDE Project](https://www.xilinx.com/html_docs/xilinx2019_2/vitis_doc/Chunk1843199917.html#cpe1508968036414) to know more about Vitis IDE.


### Description of example application

This lab uses an example application available in Vitis. It consists of a host application and kernel (written in C++/OpenCL). The kernel is a simple vector addition. The elements of 2 vectors (A & B) are added together, and the result returned in a third array (C). The host application initializes the two input arrays, send data to the kernel, and read back the result.

You will compile and check a software only version of the application. The *vector add* kernel will then be implemented as a hardware kernel. You will first build an emulation version of the design and run a simulation of the hardware kernel. You will then test the application with the kernel running in the FPGA in the next part of the lab.

## Objectives

After completing Introduction to Vitis Part 1 and 2, you will learn to:

* Create a project using the Vitis GUI
- Run Software Emulation to verify the functionality of a design
- Run Hardware Emulation to verify the functionality of the generated hardware
- Build the system and test it in hardware
- Perform profile and application timeline analysis in hardware emulation

## Steps

### Create a Vitis Project

1. Launch Vitis GUI

    Make sure Vitis and XRT environment has been setup. XRT setup is necessary before launching Vitis because building and running acceleration applications requires XRT. To do so, the following commands should return a valid path.

    ```sh
    echo $XILINX_VITIS
    echo $XILINX_XRT
    ```

    If either of the variables above are empty, then execute the following two commands:

    ```sh
    source $AWS_FPGA_REPO_DIR/vitis_setup.sh
    source $AWS_FPGA_REPO_DIR/vitis_runtime_setup.sh
    ```

1. Invoke GUI by executing the following command:

    ```sh
    vitis &
    ```
1. Set workspace to any empty folder, such as `~/workspace` and click **Launch**  

	![](./images/Vitis_intro/workspace.png)

1. The Vitis IDE Welcome page will be displayed

	![](./images/Vitis_IDE.png)

1. Create a new application project

    Use `Create Application Project` from Welcome page, or use `File > New > Application Project` to create a new application.

    ![](./images/Vitis_intro/new_application.png)

1. Click **Next >** in the first window

    ![New Application Project Name](./images/Vitis_intro/project_wizard.png)

1. Select `xilinx_aws-vu9p-f1_shell-v04261818_201920_2` platform and click **Next >**

    ![New Application Project Platform](./images/Vitis_intro/select_platform.png)

    If you do not see this platform, make sure to [set up](setup_xup_aws_workshop.md#lab-setup) `PLATFORM_REPO_PATHS` variable. Or you can include the platform manually by clicking `+` button and browse to `/home/centos/src/project_data/aws-fpga/Vitis/aws_platform/` and select `xilinx_aws-vu9p-f1_shell-v04261818_201920_2`

1. Name the project `vadd` and click **Next >**

    ![New Application Project Name](./images/Vitis_intro/project_name.png)

1. Select `Empty Application` in the *Template* window and click **Finish**

    ![](./images/Vitis_intro/template.png)

1. The project is generated.

1. In the `Explorer` view right-click on `src` under *vadd* and select **Import Sources...**

    ![](./images/Vitis_intro/import_sources.png)

1. In the new window, click *Browse* and navigate to `~/xup_compute_acceleration/sources/vadd_lab/` and click OK. Then select the **vadd_lab** folder. Finally click *Finish*

    ![](./images/Vitis_intro/add_sources.png)

    Expand the `src` folder in the `Explorer` view to verify that the files were added

1. In the `Application Project Setting` view click `Add Hardware function` (thunder icon)

    ![](./images/Vitis_intro/add_hw_function.png)

1. The window *Add Hardware Functions* will pop up, select `krnl_vadd(int *, int *, int *, unsigned int) - krnl_vadd.cpp` and click **OK*

    ![](./images/Vitis_intro/select_hw_function.png)

1. Verify that *krnl_vadd* is added as a *Hardware Function*

    ![](./images/Vitis_intro/project_dashboard.png)

### Build and Run Software Emulation

1. Set `Active build configuration:` to `Emulation-SW` on the upper right corner of *Application Project Settings* view

1. Begin build by clicking the hammer icon on top icon bar, or right click `vadd` and select `Build Project`

    ![](./images/Vitis_intro/sw_emu_build.png)

1. Run Software Emulation in GUI Mode

    To launch software emulation in GUI mode, first select the application in *Explorer* view, right click on *vadd[x86]* in *Explorer* view and select `Run As > Run Configurations...`

    ![](./images/Vitis_intro/sw_emu_run.png)

1. In the *Run configurations* window select *(x)= Arguments* tab and make sure `Automatically add binary container(s) to arguments` is selected. Finally, click **Apply** and then click **Run**

    ![](./images/Vitis_intro/args_sw_emu.png)

    Note that the host code also supports other two arguments, number of elements in the vector and debug (prints results)

1. Observe the application has run and the output is displayed in the *Console* view

    ```
    Found Platform
    Platform Name: Xilinx
    INFO: Reading ../binary_container_1.xclbin
    Loading: '../binary_container_1.xclbin'
    Trying to program device[0]: xilinx_aws-vu9p-f1_shell-v04261818_201920_2
    Device[0]: program successful!
    Running Vector add with 32768 elements
    Launching Hardware Kernel...
    Getting Hardware Results...
    TEST PASSED
    ```

## Conclusion

In this lab, you used Vitis IDE to create a project using one of the application templates. You then ran the design using the software emulation flows.

---------------------------------------
<p align="center">Copyright&copy; 2020 Xilinx</p>
