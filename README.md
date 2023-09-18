Creating a VPC with Public and Private Subnets using AWS CLI

DESCRIPTION:This script creates an Amazon Virtual Private Cloud (VPC) with two subnets (one public and one private) and links an Internet Gateway to the public subnet. Additionally, it associates a route table with the private subnet to enable communication within the VPC.

Prerequisites

    1.AWS CLI installed and configured with the necessary IAM permissions.
    2.A basic understanding of AWS networking concepts like VPCs, subnets, and route tables.

Usage

    1.Open a terminal and navigate to the directory containing the script.

    2.Make the script executable:
	-chmod +x create_vpc.sh

    3.Run the script:
	-./create_vpc.sh

    4.The script will create the following resources:
        * VPC
        * Internet Gateway
        * Public Subnet
        * Private Subnet
        * Route Table (associated with the private subnet)

    5.After execution, the script will display the VPC ID, Public Subnet ID, and Private Subnet ID.

    6.Customize the script as needed by modifying the CIDR blocks, availability zones, or other parameters to match your requirements.

Script Explanation

The script does the following:

    1.Creates a VPC with the specified CIDR block.

    2.Enables DNS support and hostname resolution for the VPC.

    3.Creates an Internet Gateway and attaches it to the VPC.

    4.Creates a public subnet within the VPC with the specified CIDR block.

    5.Creates a private subnet within the VPC with the specified CIDR block.

    6.Creates a route table for the private subnet.

    7.Adds a route to the route table for the Internet Gateway.

    8.Associates the private subnet with the route table.

Customization

You can customize the script by changing the following variables:

    vpc_cidr: The CIDR block for the VPC.
    public_subnet_cidr: The CIDR block for the public subnet.
    private_subnet_cidr: The CIDR block for the private subnet.

You can also adjust the availability zones and other parameters to match your specific requirements.
Note

    Ensure that you have configured the AWS CLI with the appropriate IAM permissions to create VPC resources.

    This script creates a basic VPC setup. For more complex configurations, consider using AWS CloudFormation or Terraform.

    Be cautious when running scripts that create AWS resources to avoid unintended charges.

