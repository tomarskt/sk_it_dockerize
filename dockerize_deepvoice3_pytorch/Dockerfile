FROM ubuntu:latest

RUN \
 sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
 apt-get update && \
 apt-get -y upgrade && \
 apt-get install -y git python3-pip python3-dev wget && \
 cd /usr/local/bin &&  \
 ln -s /usr/bin/python3 python && \
 pip3 install --upgrade pip && \
 python3 -m pip install numpy && \
 rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/r9y9/deepvoice3_pytorch.git
RUN cd deepvoice3_pytorch && pip3 install -e ".[bin]"
RUN wget https://www.dropbox.com/s/5ucl9remrwy5oeg/20180505_deepvoice3_checkpoint_step000640000.pth
RUN mv 20180505_deepvoice3_checkpoint_step000640000.pth /deepvoice3_pytorch/checkpoints
RUN ls -la /deepvoice3_pytorch && ls -la /deepvoice3_pytorch/checkpoints
