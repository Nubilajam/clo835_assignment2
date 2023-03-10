This commands will be ran to ensure we complete our task
# ssh into the EC2 instance
ssh -i assignment1-dev 54.208.25.200

# Authorizing init_kind.sh to form cluster
chmof 777 init_kind.sh

# Run the cluster
./init_kind.sh

# Verify a single cluster has create
k get nodes


#Authorizing key for secure copying
chmod 600 assignment1-dev

# Secure copying folder into tmp of EC2 instanvce
scp -i assignment1-dev again/* 54.208.25.200:/tmp/
 
# Creating vnet
alias k=kubectl
k create ns vnet

# Creating pod using manifest
k create -f sql-pod -n vnet

k create -f webapp-pod -n vnet