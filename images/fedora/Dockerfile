FROM fedora:rawhide

# RUN dnf -y update && dnf clean all
RUN dnf -y install coreutils findutils bc gnupg git

ENV DOCKER=true
RUN mkdir -p /workdir
WORKDIR /workdir

COPY .manage.yml .manage.yml
COPY LICENSE LICENSE
COPY manage manage
COPY modules modules
COPY scripts scripts
COPY tests tests
COPY vendor vendor
COPY .manage_modules .manage_modules

RUN ./manage trust-escapace
RUN mv /workdir/vendor/tini/tini /sbin/tini
RUN chown root:root /sbin/tini
RUN chmod 755 /sbin/tini

ENTRYPOINT ["/sbin/tini", "--", "/workdir/manage"]
CMD ["help"]
