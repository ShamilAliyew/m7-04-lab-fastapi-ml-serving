# API Design Decisions

## 1. Versioning

Path-based versioning was chosen because the API version is visible directly in the URL and easier for clients to understand.

It also simplifies routing, documentation, and backward compatibility when multiple API versions are supported.

## 2. Batch Ordering and Partial Failures

Batch responses preserve the same ordering as the input request.

If one image is corrupt, only that item returns an error while the remaining items are processed normally.

This avoids unnecessary retries and improves throughput for large batches.

## 3. Async Lifecycle

Jobs move through the states queued, running, completed, and failed.

Clients can poll the job endpoint until a terminal state is reached.

Completed and failed results are retained for 24 hours before automatic deletion.
