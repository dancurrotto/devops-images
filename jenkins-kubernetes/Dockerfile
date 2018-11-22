FROM jenkinsci/blueocean

#Install the aws cli
#*******************************


#I was able to follow the instructions on aws: apk add py-pip to install pip.
RUN apk update
RUN apk add py-pip
RUN pip install --upgrade pip
# And then 
RUN pip install awscli --upgrade --user       to install aws cli
# and 
RUN export PATH=~/.local/bin:$PATH      to have the installation location in the path
# If I run     ls ~/.local/bin    I see aws in there.
RUN aws --version


RUN pip install awscli --upgrade --user

#Put the installation location in the path
RUN export PATH=~/.local/bin:$PATH   

CMD aws --version

#Installing Kubernetes
#*******************************
#Generate ssh keys.
RUN ssh-keygen -t rsa -N "" -f /root/.ssh/id_rsa

#Make the SSH key available to kops
RUN cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

#Install kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

RUN chmod +x kubectl

#Add it to a directory in the PATH
RUN mv kubectl /usr/local/bin/

CMD kubectl version

#Install kops
RUN curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

RUN chmod +x kops-linux-amd64

RUN mv kops-linux-amd64 /usr/local/bin/kops

CMD kops version

