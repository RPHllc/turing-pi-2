#---
# name: text-generation-webui
# depends: [dustynv/text-generation-webui, code_syntax_highlight, chatbot_clinic,
#           dynamic_context, hello_outside_world, LLM_Web_search]
# requires: '>=36.2.0'
# docs: docs.md
#---

ARG BASE_IMAGE
FROM ${BASE_IMAGE}

# Load and configure external extensions

  WORKDIR /opt/text-generation-webui/extensions

  # Code Syntax Highlight
    RUN git clone https://github.com/DavG25/text-generation-webui-code_syntax_highlight code_syntax_highlight

  # Chatbot Clinic
    RUN git clone https://github.com/p-e-w/chatbot_clinic chatbot_clinic

  # Dynamic Context
    RUN git clone https://github.com/elPatrixF/dynamic_context dynamic_context

  # Hello Outside World
    RUN git clone https://github.com/src-r-r/hello_outside_world hello_outside_world
    # listing files by hand because the requirements.txt file has a typo.
    # RUN pip3 install --no-cache-dir --verbose -r hello_outside_world/requirements.txt
    RUN pip3 install --no-cache-dir --verbose newspaper3k requests-cache nltk

  # LLM Web Search
    RUN git clone https://github.com/mamei16/LLM_Web_search LLM_Web_search
    RUN pip3 install --no-cache-dir --verbose -r LLM_Web_search/requirements.txt

WORKDIR /

CMD /bin/bash -c "cd /opt/text-generation-webui && python3 server.py --model-dir=/data/models/text-generation-webui --listen --verbose"
