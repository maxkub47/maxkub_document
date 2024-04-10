---
title: Source Dates
sidebar_position: 2
---

Source dates are supported in Code for IBM i, but not by default.

## Prerequisites to using source dates

For source dates to be enabled, the QCCSID system value must not be 65535. See [our documentation about encoding](../../tips/ccsid/) and [IBM's documentation about the QCCSID system value](https://www.ibm.com/docs/en/i/7.5?topic=faqs-i-system-value-qccsid).

## Source date settings

Source dates can be enabled in the connection settings.

There are three options pertaining to source dates:

- _Enable Source Dates_: If source date support is enabled for source members
- _Source date tracking mode_: What type of mode should be used to track changes. More below.
- _Source Dates in Gutter_: Whether the source dates should appear in the gutter of the editor when enabled

## Tracking modes

There are two types of editing modes for source dates

- _Edit mode_ which is the traditional style for editing. When a line changes, the source date of that line will be updated. It does not understand undo/redo. It is considered the 'dumb' mode.
- _Diff mode_ is the modern approach to source date tracking. Instead of tracking edits line by line, it is doing [a diff](https://en.wikipedia.org/wiki/Diff) to understand what has changed in the document. It diffs the base document (from last open or last save) against the latest dirty version of the document. This is a Test enhancement. It does understand undo/redo. It is considered the 'smarter' mode of the two modes.

## Source date filtering

This feature is only enabled when using 'Diff mode' tracking, as well as having the source dates gutter enabled.

Hovering over the gutter will show two buttons to:

- show changes since last save, which opens a new diff view with the changes
- start a new search based on the source date

![Editing max space](../img/sourcedates_1.png)

---

Starting a search based on date will allow the user to enter a new date filter in `YYMMDD` format. The gutter will highlight any dates on or after the date the user entered.

Hovering over the gutter again will show another button to clear the filter.

There is also a button on the status bar the user can use to start a new date filter.

![Editing max space](../img/sourcedates_2.png)

---
