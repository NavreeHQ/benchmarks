# syntax=docker/dockerfile:1
# Navree benchmark API. The build context is this folder (frameworks.json); the
# app depends on the published navree crate. Dockerfile.dockerignore keeps the
# context to the manifest, the lock file, the source and the configuration.

FROM rust:1-bookworm AS build
WORKDIR /src
COPY Cargo.toml Cargo.lock ./
COPY src ./src
RUN --mount=type=cache,id=navree-bench-cargo-registry,target=/usr/local/cargo/registry \
    --mount=type=cache,id=navree-bench-cargo-git,target=/usr/local/cargo/git \
    --mount=type=cache,id=navree-bench-target,target=/src/target \
    cargo build --release --locked --jobs 6 \
    && cp target/release/navree-bench /usr/local/bin/navree-bench

FROM debian:bookworm-slim
WORKDIR /app
COPY --from=build /usr/local/bin/navree-bench /usr/local/bin/navree-bench
# config/app.toml is read from the working directory.
COPY config ./config
EXPOSE 8080
# A benchmark harness image: built and run only on a benchmarking machine, never deployed.
# nosemgrep: dockerfile.security.missing-user.missing-user
CMD ["navree-bench", "serve"]
