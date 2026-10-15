# Emails go to an outbox during the MVP

Every email Scratch would send is written to an outbox table and shown on an outbox page instead of being delivered. This lets me demo and test every notification without a verified sending domain or the risk of emailing real people. All email passes through one send function, so switching to real delivery through Resend is a change in one place.
