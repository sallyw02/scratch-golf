# Scratch

Scratch is a lightweight CRM for independent golf coaches who already have students. It keeps each coach's students, lessons, notes and follow-ups in one place.

## People

**Coach**:
An independent golf coach who signs in to Scratch and owns a private set of Students. Each Coach's data is invisible to every other Coach.
_Avoid_: User, instructor, teacher, pro

**Student**:
A person a Coach teaches, kept as a record the Coach manages. A Student has an email address but no account and never signs in.
_Avoid_: Client, customer, member

**Group**:
A label a Coach creates and assigns to Students by hand, such as "Juniors". A Student can belong to several Groups.
_Avoid_: Segment, tag, category

**Needs Attention**:
The state of a Student who has no upcoming Lesson and whose last completed Lesson was more than the Coach's chosen number of days ago (30 by default). A Student with no Lessons at all needs attention 14 days after being added.
_Avoid_: At risk, inactive, churned, lapsed

## Lessons

**Lesson**:
A single scheduled session between a Coach and one Student, kept on the Coach's calendar.
_Avoid_: Booking, appointment, session

**Lesson Status**:
Where a Lesson stands: Scheduled, then exactly one of Completed, Cancelled or No-show. Rescheduling changes a Scheduled Lesson's time and does not change its status.
_Avoid_: State, outcome

**Lesson Note**:
The written summary a Coach sends a Student after a Lesson, covering a focus area, assigned drills and an optional swing video link.
_Avoid_: Report, recap, feedback

**Swing Video Link**:
A link to a video hosted elsewhere, such as YouTube or Google Drive. Scratch stores the link, never the video.
_Avoid_: Video, upload

**Follow-up Thread**:
The short message exchange attached to one Lesson. The Coach writes in it inside Scratch, and the Student replies through a private link without signing in.
_Avoid_: Chat, conversation, messages
