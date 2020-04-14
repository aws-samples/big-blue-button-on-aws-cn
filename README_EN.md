# BigBlueButton on AWS 

BigBlueButton is an online conference system. You can use this solution to provision an online web conference system
automatically, or you can combine this with our previously published 
[Moodle on AWS CN](https://github.com/aws-samples/moodle-on-aws-cn). Through the combination with Moodle, we can quickly 
deploy a complete e-learning solution. 

- **Supported Regions:** cn-north-1(Beijing), cn-northwest-1(Ningxia)
- **Version:** v1.0
- **Estimated Deployment Time:** 60min

## Architect

You can choose to deploy the Web Conference system directly, or deploy with the Moodle solution. The following 
is the architecture diagram.

![Architect](assets/architecture.png). 

## Deployment Prerequisites

1. This solution provides a one-click deployment solution for BigBlueButton in the AWS China region. 
BigBlueButton is under the [GNU Lesser General Public License V3 (LGPLv3)](https://www.gnu.org/licenses/lgpl-3.0.html), 
By deploy the BigBlueButton through this solution, you agrees to the [BigBlueButton license](https://bigbluebutton.org/open-source-license/).

2. Prepare ICP-registered domain names. Deploying Web services in Mainland China requires an ICP-registered domain 
name to run your business legally. Please prepare the domain name filed by ICP in advance.

3. 2 Elastic IPs. These 2 Elastic IPs are used for Turn Server and App Server respectively.

4. Configure DNS resolution. Configure DNS so that the domain names of Turn Server and App Server point 
to two Elastic IPs respectively.

## Step 1: Launch CloudFormation Stack

This automated AWS CloudFormation template deploys the BigBlueButton application on AWS Cloud.

You are responsible for the cost of AWS services used when running this solution. For more details, please see the "Fee" 
section. For full details, see the pricing page for each AWS service that will be used in this solution.

1. Log in to the AWS Management Console and click the button below to launch the AWS CloudFormation template.

    [![Launch Stack](launch-stack.png)](https://cn-northwest-1.console.amazonaws.cn/cloudformation/home?region=cn-northwest-1#/stacks/create/template?stackName=BigBlueButton&templateURL=https:%2F%2Faws-solutions-reference.s3.cn-north-1.amazonaws.com.cn%2Fbig-blue-button-on-aws%2Flatest%2F00-master.template)
    
1. By default, the template is launched in the AWS Ningxia region. To start the solution in other AWS regions, use the 
region selector in the navigation bar of the console.

1. On the **Create Stack** page, confirm that the correct template URL is displayed in the **Amazon S3 URL** text box, and then choose **Next**.

1. On the **Specify Stack Details** page, assign a name to the solution stack.

1. Under **Parameters**, view the parameters of the template and modify them as needed. This solution uses the following default values.

    **General AWS**

    | Parameter            | Default    | Description                                                  |
    | --------------- | --------- | ----------------------------------------------------- |
    | EC2 Key Pair    |           | EC2 Key Pair name, used to SSH access to instance |
    | SSH Access From | 0.0.0.0/0 | Allowed IP range to SSH from for Bastion Security Group            |

    **Network**

    | Parameter                         | Default        | Description                                                         |
    | ---------------------------- | ------------- | ------------------------------------------------------------ |
    | VPC ID                       |               | Choose existing VPC                                        |
    | Subnet ID                    |               | Choose existing Subnet, must be a public subnet                          |

    **BigBlueButton General Information**

    | Parameter                 | Default         | Description                                     |
    | -------------------- | -------------- | ---------------------------------------- |
    | Email                |                | Used for Let's encrypt SSL       |
    | Secret ID            | 12345678       | Inter-communication between Turn and App servers     |

    **Turn Server**

    | Parameter               | Default      | Description               |
    | ------------------ | ----------- | ------------------ |
    | Instance Size      | c5.large    | Turn instance size     |
    | Domain Name        |             | Turn Server domain      |
    | EIP Allocation ID  |             | EIP  Allocation ID      |
    | Disk Size          | 100         | Disk size     |

    **App Server**

    | Parameter               | Default      | Description               |
    | ------------------ | ----------- | ------------------ |
    | Instance Size      | c5.2xlarge    | App instance size     |
    | Domain Name        |             | App Server domain      |
    | EIP Allocation ID  |             | EIP 的 Allocation ID      |
    | Disk Size          | 100         | Disk size     |

2. Choose **Next**。

3. On the **Configure Stack Options** page, choose **Next**.

4. On the **Review** page, review and confirm the settings. Make sure to check the box that confirms 
that the template will create AWS Identity and Access Management (IAM) resources.

5. Select **Create Stack** to deploy the stack.

You can check the status of the stack in the **Status** column of the AWS CloudFormation console. 
You should see the status as CREATE_COMPLETE in about 60 minutes.
