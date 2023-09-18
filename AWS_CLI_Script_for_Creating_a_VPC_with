#!/bin/bash

###############################
# Author: Gwhiz
# Version: v1

# This script creates an Amazon Virtual Private Cloud (VPC) with two subnets (one public and one private) and links an Internet Gateway to the public subnet. 


# Set your desired VPC and subnet CIDRs
vpc_cidr="10.0.0.0/16"
public_subnet_cidr="10.0.0.0/24"
private_subnet_cidr="10.0.1.0/24"

# Create the VPC
vpc_id=$(aws ec2 create-vpc --cidr-block "$vpc_cidr" --query 'Vpc.VpcId' --output text)

# Enable DNS support and hostname for the VPC
aws ec2 modify-vpc-attribute --vpc-id "$vpc_id" --enable-dns-support "{\"Value\":true}"
aws ec2 modify-vpc-attribute --vpc-id "$vpc_id" --enable-dns-hostnames "{\"Value\":true}"

# Create the Internet Gateway
gateway_id=$(aws ec2 create-internet-gateway --query 'InternetGateway.InternetGatewayId' --output text)

# Attach the Internet Gateway to the VPC
aws ec2 attach-internet-gateway --vpc-id "$vpc_id" --internet-gateway-id "$gateway_id"

# Create a public subnet
public_subnet_id=$(aws ec2 create-subnet --vpc-id "$vpc_id" --cidr-block "$public_subnet_cidr" --availability-zone us-east-1a --query 'Subnet.SubnetId' --output text)

# Create a private subnet
private_subnet_id=$(aws ec2 create-subnet --vpc-id "$vpc_id" --cidr-block "$private_subnet_cidr" --availability-zone us-east-1b --query 'Subnet.SubnetId' --output text)

# Create a route table for private subnet
route_table_id=$(aws ec2 create-route-table --vpc-id "$vpc_id" --query 'RouteTable.RouteTableId' --output text)

# Add a route to the route table for the Internet Gateway
aws ec2 create-route --route-table-id "$route_table_id" --destination-cidr-block "0.0.0.0/0" --gateway-id "$gateway_id"

# Associate the private subnet with the route table
aws ec2 associate-route-table --subnet-id "$private_subnet_id" --route-table-id "$route_table_id"

# Print VPC and subnet IDs
echo "VPC ID: $vpc_id"
echo "Public Subnet ID: $public_subnet_id"
echo "Private Subnet ID: $private_subnet_id"

