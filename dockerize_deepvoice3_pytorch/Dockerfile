FROM ubuntu:latest

RUN \
 sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
 apt-get update && \
 apt-get -y upgrade && \
 apt-get install -y git python3-pip python3-dev wget libasound2-dev python3-numpy python3-setuptools libsndfile-dev && \
 cd /usr/local/bin &&  \
 ln -s /usr/bin/python3 python && \
 pip3 install --upgrade pip && \
 python3 -m pip install librosa && \
 python3 -m pip install numpy && \
 rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/r9y9/deepvoice3_pytorch.git
RUN cd deepvoice3_pytorch && pip3 install -e ".[bin]"
RUN wget https://www.dropbox.com/s/5ucl9remrwy5oeg/20180505_deepvoice3_checkpoint_step000640000.pth
RUN mkdir -p /deepvoice3_pytorch/checkpoints && mv 20180505_deepvoice3_checkpoint_step000640000.pth /deepvoice3_pytorch/checkpoints/20180505_deepvoice3_checkpoint_step000640000.pth
RUN ls -la /deepvoice3_pytorch && ls -la /deepvoice3_pytorch/checkpoints
RUN wget https://www.dropbox.com/s/0ck82unm0bo0rxd/20180505_deepvoice3_ljspeech.json
RUN mv 20180505_deepvoice3_ljspeech.json /deepvoice3_pytorch/presets/20180505_deepvoice3_ljspeech.json
RUN ls -la /deepvoice3_pytorch && ls -la /deepvoice3_pytorch/presets
RUN wget https://raw.githubusercontent.com/nltk/nltk_data/gh-pages/packages/tokenizers/punkt.zip
RUN wget https://raw.githubusercontent.com/nltk/nltk_data/gh-pages/packages/corpora/cmudict.zip
RUN mkdir -p /deepvoice3_pytorch/data && cd /deepvoice3_pytorch/data && wget https://data.keithito.com/data/speech/LJSpeech-1.1.tar.bz2 && tar xvf LJSpeech-1.1.tar.bz2 && rm LJSpeech-1.1.tar.bz2 && ls -la
RUN cd deepvoice3_pytorch && python3 preprocess.py --preset=presets/20180505_deepvoice3_ljspeech.json ljspeech ./data/LJSpeech-1.1/ ./data/ljspeech
COPY sentenses.txt /deepvoice3_pytorch/sentenses.txt
RUN cd deepvoice3_pytorch && python3 synthesis.py --preset=presets/20180505_deepvoice3_ljspeech.json   ./checkpoints/20180505_deepvoice3_checkpoint_step000640000.pth   sentences.txt   output_dir
