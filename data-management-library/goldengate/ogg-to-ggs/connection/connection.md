# Create a trusted connection between Oracle GoldenGate and OCI GoldenGate

## Introduction

This lab walks you through the steps to download the root certificate from Oracle Cloud Infrastructure (OCI) and add it to the Oracle GoldenGate Service Manager. Adding the Oracle Cloud Infrastructure root certificate to Oracle GoldenGate creates a trusted TLS connection between OCI GoldenGate and Oracle GoldenGate.

Estimated time: 10 minutes

### Objectives

In this lab, you will:

* Download the root certificate for Oracle Cloud Infrastructure from your web browser to your local machine
* Add the certificate to Oracle GoldenGate's Administration Server
* Create a credential on Oracle GoldenGate to connect to OCI GoldenGate

### Prerequisites

To successfully complete this lab, you must have:

* An on premises or Marketplace Oracle GoldenGate instance running
* The URL and log in credentials for the Oracle GoldenGate Service Manager
* The log in credentials for the OCI GoldenGate Deployment Console

## Task 1A: Using Chrome to download the root certificate

The following instructions show you how to download the Root Certificate using a Chrome web browser in Windows.

> **Note:** *Mac users should follow Task 1B and use FireFox to download the root certificate.*

1.  Log in to the **Oracle Cloud Infrastructure Console** with your username and password. See [Signing in to the Console](https://docs.cloud.oracle.com/en-us/iaas/Content/GSG/Tasks/signingin.htm) in the *Oracle Cloud Infrastructure* documentation.

2.  In your Chrome browser address bar, click the padlock icon, and then click **Certificate (Valid)**.

    ![](images/01-04-certificate.png " ")

3.  In the Certificate window, click **Certification Path**, select **DigiCert**, and then click **View Certificate**.

    Another Certificate window opens, displaying the details for the root DigiCert certificate.

    ![](images/01-04-digicert.png " ")

4.  Click **Details**, and then click **Copy to File**.

    ![](images/01-05.png " ")

5.  In the Certificate Export Wizard, click **Next**.

6.  Select **Base-64 encoded X.509 (.CER)**, and then click **Next**.

    ![](images/01-07.png " ")

7.  Click **Browse** to select a location on your local machine to save the root certificate, and then enter a file name, such as **DigiCert-Root.cer**, and click **Save**.

8.  Click **Next**, and then click **Finish**.

A Certificate Export Wizard dialog displays **The export was successful**. You can close the Certificate windows.

## Task 1B: Using FireFox to download the root certificate

The following instructions show you how to download the Root Certificate using a FireFox web browser.

1.  Log in to the **Oracle Cloud Infrastructure Console** with your username and password. See [Signing in to the Console](https://docs.cloud.oracle.com/en-us/iaas/Content/GSG/Tasks/signingin.htm) in the *Oracle Cloud Infrastructure* documentation.

2.  In your FireFox browser address bar, click the padlock icon, and then next to Connection Secure, click **Show connection details** (right arrow icon).

    ![](images/01b-02.png " ")

3.  In the **Connection Security** dialog, click **More information**.

    ![](images/01b-03.png " ")

4.  In the **Page info** window, click **View Certificate**.

    ![](images/01b-04.png " ")

5.  On the **Certificate** page, click **DigiCert Global Root CA**.

    ![](images/01b-05.png " ")

6.  Under the **Miscellaneous** section, for Download, click **PEM (cert)**, and save the PEM file to your local drive.

    ![](images/01b-06.png " ")

## Task 2: Upload the certificate to the Oracle GoldenGate Marketplace Service Manager

1.  Open the on premises or Marketplace Oracle GoldenGate Service Manager in a browser window.

> **Note:** *To open the Marketplace Oracle GoldenGate Service Manager, use the Public IP of the Marketplace Oracle GoldenGate compute instance from the Oracle Cloud Console, and then enter `<public-ip>:<port 443>` in your browser address bar.*

2.  In the navigation menu (hamburger icon), click **Certificate Management**.

    ![](images/02-01-certmgmt.png " ")

3.  On the Certificate Management page, click **Add CA Certificates** (plus icon).

    ![](images/02-03-addcert.png " ")

4.  In the Add CA Certificate dialog, enter a **Unique Name**.

    ![](images/02-04-addcertdialog.png " ")

5.  For **Certificate PEM**, if you downloaded the root certificate from Chrome, open it in a text editor, and then copy and paste the key into the **Enter** text area.

    ![](images/02-05-entercert.png " ")

6.  If you downloaded the root certificate from FireFox, click **Upload**, and then click **Browse**. Locate and select the PEM file on your local machine, and then click **Upload**.

    ![](images/02-06-uploadcert.png " ")

7.  Click **Add**.  The certificate now appears in the Shared list.

    ![](images/02-07-certlist.png " ")

## Task 3: Add a credential for Oracle GoldenGate to connect to OCI GoldenGate

1.  Sign in to the OCI GoldenGate Deployment Console, and then use the Navigation menu (hamburger icon) to open the Administration Server's **Administrator** page.

    ![](images/03-01.png " ")

2.  Click **Add User** and create a user account that Oracle GoldenGate will use to connect to OCI GoldenGate. For example, name the user **ggsnet** and assign the user the Operator role.

    ![](images/03-02.png " ")

    ![](images/03-02b.png " ")

3.  On the on-premises or Marketplace Service Manager Overview page, locate the Administration Server, and then click the link in the Port column. The on premises or Marketplace Administration Server opens in a new browser.

4.  Sign in to the on-premises or Marketplace Oracle GoldenGate Administration Server with the same credentials used to log in to the Service Manager, and then use the Navigation menu to open the **Configuration** screen.

5.  Under the Database tab, click **Add Credential**, and then complete the following fields:

    * For **Credential Domain**, enter a name to distinguish this connection, such as **GGSNetwork**.
    * For **Credential Alias**,  enter a name, such as **ogg2ggs**.
    * For **User ID**, enter the user name of the user you created in step 2 (ggsnet).
    * For **Password**, enter the password associated to the user entered for User ID.
    * For **Verify Password**, re-enter the password for verification purposes.

    ![](images/03-04.png " ")

6.  Click **Submit**. You should now have two credentials in the Marketplace Oracle GoldenGate instance, one to connect to OCI GoldenGate, and one for the source database.

    ![](images/03-05.png " ")

In this lab, you created a trusted connection between Oracle GoldenGate and OCI GoldenGate using a self-signed certificate. You may now **proceed to the next lab**.

## Acknowledgements
* **Author** - Jenny Chan, Consulting User Assistance Developer, Database User Assistance
* **Contributors** -  Werner He and Julien Testut, Database Product Management
* **Last Updated By/Date** - Jenny Chan, September 2021
