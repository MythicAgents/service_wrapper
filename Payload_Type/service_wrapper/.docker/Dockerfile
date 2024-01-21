FROM itsafeaturemythic/mythic_python_base:latest as builder

COPY [".docker/requirements.txt", "requirements.txt"]
RUN python3 -m pip wheel --wheel-dir /wheels -r requirements.txt

FROM python:3.11-slim-bullseye

# Mono: 6.12

RUN apt-get update && apt-get install --no-install-recommends gnupg -y && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
  && echo "deb http://download.mono-project.com/repo/debian buster/snapshots/6.12 main" > /etc/apt/sources.list.d/mono-official.list \
  && apt-get update \
  && apt-get install -y clang nuget \
  && apt-get install -y mono-devel=6.12\* \
  && rm -rf /var/lib/apt/lists/* /tmp/*

COPY --from=builder /wheels /wheels
RUN pip install --no-cache /wheels/*

WORKDIR /Mythic/

COPY [".", "."]
# prep download any necessary nuget packages
RUN cd service_wrapper/agent_code && nuget restore

CMD ["python3", "main.py"]