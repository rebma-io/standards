# Part Numbers and Bill of Material

## Part Number Design

The general design of the part number in use is:

`<project>.<component>.<version>`

Each component is:

* `<project>`. The project represents some logical grouping of a set of parts.
  For example, the microphone is a project. To collect lots of common parts,
  parts which can be part of lots of different, the projects `000`-`099` are
  used to potentially hold lots of common parts. (regex: `\d{3}`)
* `<component>`. This can be either an assembly or a part. An assembly is
  composed of multiple other parts or assemblies. The first digit tells you
  whether the thing is an assembly or not. All assemblies start with a zero,
  where `1`-`9` is used for individual parts. (regex: `\d{4}`)
* `<version>`. A sequential identifier of the version. This is only incremented
  when a version is "approved" and used for a specific project in some way.
  Something that hasn't even been designed yet can be designated `000`. (regex:
  `\d{3}`)

This means the length of the part number is 3+1+4+1+3 = 12 characters. So, for
example, this is a part number:

`103.0033.01`

It refers to revision 1 of assembly 33 on project 103.

Note that this system does not account for different vendors. Realistically, if the parts are interchangeable, then it shouldn't matter, and if they aren't, then they aren't the same part anyway.

## Product Breakdown Structure

Every project should have a product breakdown structure (PBS). This is the authoritative list of parts and components within the project, but also represents their state. This should be kept in a spreadsheet that is easily discoverable. Some additional fields that should be kept:

1. A description of what the thing is. This is a human consumable thing.
2. What kind of thing is it? Is it an assembly, an off-the-shelf part, a
   designed (custom) part, or a piece of hardware. 
3. What's the build strategy? Is it just purchased (off-the-shelf), 3D printed,
   machined, fabricated, or out-sourced to a third-party for construction. 
4. What is the source of the part? This typically is a vendor, but for small
   things (like a screw, for example), this could just be "inventory". 
5. Quantity needed per unit of the project. For example, if a project uses 2 of
   one part, and you build 10 of the project, then your PBS would show 2, but
   your order would be for 20.
6. Current status of the part. This could be not designed, design-in-progress,
   designed, needs rework (meaning a design has been done, evaluated, but needs
   to be reworked), ready to order, ordered, received, completed, or assembled.
   Finally, it could also be cancelled. Since part numbers shouldn't be re-used,
   ever, something that is eventually unused goes to cancelled. For parts, this
   will eventually end up on completed or received, but assemblies will always
   end on assembled. 