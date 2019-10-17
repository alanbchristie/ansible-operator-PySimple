FROM quay.io/operator-framework/ansible-operator:v0.11.0

RUN ansible-galaxy install alanbchristie.pysimple
COPY watches.yaml ${HOME}/watches.yaml
