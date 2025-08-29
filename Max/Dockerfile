# --- Build Stage ---
FROM rust:1.81 as builder

# Set working directory
WORKDIR /usr/src/stalin-sort

# Copy manifests first (für bessere Layer-Caching-Effizienz)
COPY Cargo.toml Cargo.lock ./

# Create a dummy main.rs, damit cargo build --release dependencies cachen kann
RUN mkdir src && echo "fn main() {}" > src/main.rs && cargo build --release && rm -rf src

# Copy actual source
COPY src ./src

# Build release binary
RUN cargo build --release

# --- Runtime Stage ---
FROM debian:bookworm-slim

# Copy binary from builder
COPY --from=builder /usr/src/stalin-sort/target/release/stalin-sort /usr/local/bin/stalin-sort

# Run the binary by default
CMD ["stalin-sort"]
