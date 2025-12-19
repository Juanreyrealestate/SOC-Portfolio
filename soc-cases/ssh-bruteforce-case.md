# Multiple Failed SSH Authentication Attempts

## Summary
Multiple failed SSH login attempts were detected targeting invalid users from a single source within a short time window.

## Detection Source
Authentication logs located at `/var/log/auth.log`.

## Timeline
- Failed SSH login attempts for invalid user `fakeuser` originating from `127.0.0.1`.
- Repeated attempts observed within a short time interval.

## Analysis
The repeated failed authentication attempts targeting invalid users in a short time window are consistent with brute force behavior.

## Severity and Confidence
- Severity: Low–Medium  
- Confidence: High

## Action Taken
Activity was monitored. No successful authentication was observed.

## Recommendation
Continue monitoring. Implement threshold-based alerting or temporary blocking if activity increases.
