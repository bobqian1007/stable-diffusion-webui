FROM nvidia/cuda:11.4.3-cudnn8-runtime-ubuntu20.04

# Install Python and other dependencies
RUN apt-get update && apt-get upgrade -y && apt-get install -y python3 python3-pip && apt-get install -y vim git

#RUN DISTRIBUTION=`dpkg --status tzdata|grep Provides|cut -f2 -d'-'` && \
#    echo "deb http://mirrors.aliyun.com/debian/ ${DISTRIBUTION} main non-free" > /etc/apt/sources.list && \
#    apt-get update && \
#    apt-get upgrade -y && \
#    apt-get install -y vim git

ARG PYPI=https://mirrors.aliyun.com/pypi/simple
ARG target=/stable_deffusion_web_ui
COPY requirements_versions.txt /tmp/
COPY requirements_codeformer.txt /tmp/
RUN python3 -m pip install https://files.pythonhosted.org/packages/86/41/00a6b000f222f0fa4c6d9e1d6dcc9811a374cabb8abb9d408b77de39648c/basicsr-1.4.2.tar.gz
RUN python3 -m pip install -i ${PYPI} git+https://github.com/TencentARC/GFPGAN.git@8d2447a2d918f8eba5a4a01463fd48e45126a379 --prefer-binary
RUN python3 -m pip install -i ${PYPI} git+https://github.com/openai/CLIP.git@d50d76daa670286dd6cacf3bcd80b5e4823fc8e1 --prefer-binary
RUN python3 -m pip install -i ${PYPI} git+https://github.com/mlfoundations/open_clip.git@bb6e834e9c70d9c27d0dc3ecedeebeaeb1ffad6b --prefer-binary
RUN python3 -m pip install --no-cache-dir -i ${PYPI} -r /tmp/requirements_codeformer.txt --prefer-binary
RUN python3 -m pip install --no-cache-dir -i ${PYPI} -r /tmp/requirements_versions.txt --prefer-binary



WORKDIR ${target}

COPY textual_inversion_templates/ textual_inversion_templates/
COPY test/ test/
COPY scripts/ scripts/
COPY modules/ modules/
COPY javascript/ javascript/
COPY html/ html/
COPY extensions-builtin/ extensions-builtin/
COPY configs/ configs/

RUN mkdir repositories
RUN mkdir models
RUN mkdir localizations
RUN mkdir extensions
RUN mkdir embeddings

COPY launch.py ./
COPY script.js ./
COPY style.css ./
COPY webui.py ./
COPY webui_simplified.sh ./






