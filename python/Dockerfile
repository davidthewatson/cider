FROM alpine as intermediate

  
RUN apk add --no-cache git \
      git-doc

RUN git clone https://github.com/powerline/fonts.git --depth=1
WORKDIR /fonts
RUN ./install.sh
WORKDIR /
RUN rm -rf fonts

ARG GITHUB_TOKEN
RUN git config --global url."https://${GITHUB_TOKEN}:@github.com/".insteadOf https://github.com/
ARG GITHUB_REPOSITORY
RUN git clone ${GITHUB_REPOSITORY}

FROM python:3.7.0-alpine3.8

COPY --from=intermediate / .

RUN apk add --no-cache openssh \
      emacs \
      tmux \
      fish \
      man \
      curl

WORKDIR /

ADD .tmux.conf /root/.tmux.conf
ADD config.fish /root/.config/fish/config.fish
RUN curl -Lo ~/.config/fish/functions/fisher.fish --create-dirs https://git.io/fisher

WORKDIR /backend

RUN git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done

RUN git pull --all

RUN fish -c "fisher matchai/spacefish"

ENTRYPOINT ["tmux"]
