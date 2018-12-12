# Proposal: Non-Standard Schemes for Module Resolution in Node.js

**Contributors**: <!-- Saleh Abdel Motaal (@SMotaal) -->

## Motivating Examples

- An ESM loader implementation with an underlying and non-deprecated module system, like Node.js, which uses non-standard module specifiers — for backwards-compability and transparent interoperability with existing systems.

- An ESM loader implementation with custom loader extensions, where more than one module resolution systems will potentially need to delegate aspects of module resolution to the respective extensions — for decoupled interoperability between custom loader extensions.

  Extensions can include:

  1. A custom ESM loader extension wrapping an existing module system which uses non-standard module specifiers using a "hidden" specifier adaptation bridge — for non-obtrusive resolution relay across systems.

  2. A custom ESM loader extension adding support for modules which use standard module specifiers to an ESM loader implementation that does not normally support such schemes — for interoperability with user-configured protocols.

  3. A custom ESM loader extension adding support for modules which enforce certain security requirements (ie using handles) for a scoped subset of the default scheme and must retain full bi-directional control over all resolutions within the given scope  — for certified access to encrypted sources.

## High Level Concerns

1. ECMAScript and other module systems may interpret specifiers differently and incorrectly if a specifier is handled by the wrong operator.

2. A non-standard specifier interpreted by the intended system can resolve to an absolute location inteded for a specific resource loader, leading to unpredictable outcomes if handled by the wrong operator.

3. A custom loader extension handling special specifiers:

   1. Accidentally claim or relay a module request to a wrong custom loader.

   2. Handle an intent of specifiers differently from other custom loaders.

   4. Involving path-based specifiers which may be inconsistently converted from and to a default specifier notation, ie URLs.

4. A custom loader extension handling special resources:

   1. Unwittingly disclose or miliciously acquire information about modules.

   2. In a user-configured extensible ESM loader system handling ambigious and non-explicit specifiers, leading to unreliable partitioning that can be misappropriated by others or avoided for such applications.

## Scope

Prior to the realization of a standard ECMAScript Module, every module system introduced a module specifiation machanism that best leveraged its the unique conditions of its environment.

We don't think about it much, but in the purest sense, such a mechnaism that uses deterministic algorithms to determine an absolute location of a resource based on a qualified specifier string and one or more well-defined conditions of the operating environment, is functionally a non-standard scheme.

While no one can claim that such mechanisms are in fact schemes, no one can also deny that for the ones that specifically adhere to the above criteria, they are as close to schemes enough to earn some affilated term of their own.

At the same time, and purely from the narrow-perspective of module resolution within the JavaScript ecosystem, the rest of those mechanisms remain to be a fact of life, and they too cannot be excluded from the ecosystem, earning them a term as well.

This proposal focuses on the challenges that can impede interoperability between a conforming ECMAScript Module module system and other systems which historically operated with non-standard module specifiers.

### Stipulative Terms

<dl><lh><em>

**Non-Standard Scheme**, module specifiers using …

</em></lh><ul>

<dt>Symbolic Scheme<dd>

A symbolic scheme is a deterministic specifier resolution mechanism for which the explicit or implicit scheme part of its locators is neither a standard or registered scheme.

<dt>Arbitrary Scheme<dd>

An arbitrary scheme is a potentially non-deterministic specifier resolution mechanism for which the explicit or implicit scheme part of its locators is neither a standard or registered scheme.

<dt>Ambigious Scheme<dd>

An ambigious scheme is the term used to identify schemes which are not known in the context of a resolver, where a resolver is not able to determine the actual classification for a non-standard scheme, specifically if it is symbolic or arbitrary scheme.

</ul>

<lh><em>

**Scheme Part**, a module specifier's …

</em></lh><ul>

<dt>Explicit Scheme Part<dd>

The leading portion of an absolute URL up to and including the colon, ie <samp>http:</samp> or <samp>file:</samp>, which forces a specifier resolution mechanism to not default to the scheme of a referring URL when attempting to resolve the absolute location of a URL.

<dt>Implicit Scheme Part<dd>

An implicit scheme part is an assumed scheme part attributed to a specifier when the specifier does not include an explicit scheme part, and is normally determined by the explicit scheme part of a referring URL, and in theory as proposed, where that is not applicable, an implicit default scheme reflecting a prescribed symbolic or arbitrary scheme implementation.
</dl>

## Proposal

**TBD**


<!--
## TL;DR In a hurry?

Just read the [Proposal](#proposal) section.
-->
