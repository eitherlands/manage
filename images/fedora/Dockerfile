FROM fedora:rawhide
MAINTAINER Mark Milstein <mark@epiloque.com> (@epiloque)

# RUN dnf -y update && dnf clean all
RUN dnf -y install coreutils findutils bc

ENV DOCKER=true
RUN mkdir -p /workdir
WORKDIR /workdir

COPY .manage.yml .manage.yml
COPY LICENSE LICENSE
COPY bin bin
COPY modules modules
COPY scripts scripts
COPY test test
COPY vendor vendor

RUN mv /workdir/vendor/dumb-init/dumb-init /usr/bin/dumb-init
RUN chown root:root /usr/bin/dumb-init
RUN chmod 755 /usr/bin/dumb-init

ENTRYPOINT ["/usr/bin/dumb-init", "--", "/workdir/bin/manage"]
CMD ["help"]