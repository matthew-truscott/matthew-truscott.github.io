---
title: "Trampolines"
date: 2016-10-10T10:10:00Z
categories: applied_math diff_eq
math: false
draft: false
---

There is a form of differential equation I never went into last time, I will generate it again, this time through a different stand-alone example. Trampolines are a great way to see the use of such equations in the real world. First let's ignore how they work and consider what they do. A trampoline is a large area of fabric that remains stretched out. When someone stands on the surface, the fabric gets pulled in, so that their feet are lower than the surface was originally. When someone jumps on the trampoline, the surface pushes back and allows them to jumps higher. Without any extra legwork, a person may remain bouncing for a little while, however, normally they'll need to put in some effort in order to continue bouncing. How is this all possible?

The basic physics explanation is neat and simple. Trampolines exploit the nature of springs. Springs have some natural length, change this, and they supply a restoring force proportional to the length of contraction of expansion. Multiple springs are used, not only to fit the shape of the trampoline, but also so that each spring need not be as strong. Each spring has some tolerance, supply too much force (extend it too much) and they lose their ability to pull back. If you use springs together in parallel, the force each experiences, assuming the springs are identical, is split evenly. Let's first consider a trampoline without a person standing on it. We will assume that one spring is in operation, (which is okay as long as they are identical), and that the fabric weighs nothing.

Constructing the equation is straightforward, if force is proportional to extension, $$F=-kx$$ where k is a constant. Note the negative sign to denote a restoring force. As we have seen before, \\(F = ma\\) and \\(a\\) is just a second derivative of \\(x\\), so

$$\frac{d^2x}{dt^2} = -\frac{k}{m}x$$

### Second Order Differential Equations

Let's go ahead and solve this, the result will be a relation between spring extension and time. Since spring extension is proportional to the height of the trampoline, the result will also describe this height. Second order differential equations are not easy to solve. The trick is to put them into a familiar form and then perform 'standard techniques' on the result. First group all instances of x onto one side. If anything else exists, the equation is inhomogeneous and requires extra work. We'll come back to that. If the right hand side is zero, the equation is homogenous. I will start with an intuitive way to solve the problem. Take a step back and consider the equation as is was first constructed. It is clear that the second derivative of x is proportional to x. Therefore it seems reasonable to want to find some function, that differentiates twice to give itself, multiplied by some factor. What functions do this?

The correct answer is of course an oscillating function typically described by a linear combination of sine and cosine functions. Take sine:

$$\frac{d\sin(\alpha t)}{dt} = \alpha\cos(\alpha t)$$

$$\frac{d^2\sin(\alpha t)}{dt^2} = -\alpha^2\sin(\alpha t)$$

Clearly in our case,

$$\alpha = \sqrt{\frac{k}{m}}$$

so

$$x = A\sin(\sqrt{\frac{k}{m}}t + \phi)$$

I also added constants \\(\phi\\) and \\(A\\) since these do not create any extra terms during differentiation.

![]("https://upload.wikimedia.org/wikipedia/commons/thumb/d/d2/Sine_one_period.svg/600px-Sine_one_period.svg.png")

The above gives the shape of such a curve. What values the constants end up taking depend on the initial conditions. In order to solve for three unknowns \\(A\\), \\(\phi\\) and \\(t\\), we need three pieces of information. At some given it is necessary to know both the position and the velocity of the system (or the position at one time and the velocity at another time). The velocity is simply the derivative of the position. Clearly if the velocity and the position are zero at any time, the only possible configuration is \\(A = 0\\) and the trampoline never moves! But otherwise it takes a shape like in the graph.

### Damping

Of course in reality the trampoline never continues to wobble ad infinitum, so we need to modify our model somewhat in order to get a more accurate representation. Like with last time, there is some opposing force involved which takes energy from the system, this one we usually call friction. I will not go into the math just yet. Let's return to the simple trampoline again. Mathematically, how do you solve differential equations of this form? This applies to any order, but typically we use it for second-order equations because higher-orders get nasty. Say you have an equation of the form

$$a\frac{d^2y}{dx^2} + b\frac{dy}{dx} + cy = 0$$

where all the derivative terms are linear (you can extend this for higher powers no problem), the form that \\(y\\) takes is surprisingly simple. If all the terms are indeed linear, y has to look like an exponential of some kind. The derivatives of exponentials are all proportional in some way, so when you substitute them in to the differential equation, the exponent part simply cancels and you're left with a polynomial! Second-order linear differential equations are clearly nice because they reduce to quadratic equations which are easy to solve. So let's suppose \\(y = K\exp mx\\) where \\(K\\) and \\(m\\) are constants. Plugging this into the differential equation gives

$$Kam^2\exp(mx) + Kbm\exp(mx) + Kc\exp(mx) = 0$$

the exponent part indeed cancels, along with the constant and we are left with

$$am^2 + bm + c$$

Since we want to find m, put this into the quadratic equation.

$$m = \frac{-b\pm\sqrt{b^2 - 4ac}}{2a}$$

Now it's worth considering what different values m could take. Hopefully you're familiar with the possible outputs from the quadratic equation. Note that we do consider the possibility of complex roots. Therefore there are three different types of solutions. Two real roots imply that there are two possible solutions to the differential equation, call these \\(A\exp(m\_+x)\\) and \\(A\exp(m\_-x)\\). One can combine these by the principle of superposition (if there are multiple solutions, then a linear combination of them must also be a solution). So the general solution would be written something like

$$A\exp(m_+x) + B\exp(m_-x)$$

If there is only one root (that is, they are repeated), we find another solution by adding a linear component (I don't think it's very important to understand why this is the case, just know that if this linear component causes a conflict, use a quadratic component and so on...), it's possible to write a general solution

$$(A + Bx)\exp(mx)$$

If the roots are complex, separate each into real and imaginary parts. Clearly they will share the same real part, and the solutions are

$$A\exp(nx)\exp i(c_+x)$$

and

$$A\exp(nx)\exp i(c_-x)$$

where \\(c\_\pm\\) are the imaginary components to \\(m\\) and \\(n\\) is the real part. Combine these using superposition to obtain

$$\exp(nx)(A\exp i(c_+x) + B\exp i(c_-x))$$

Now

$$\exp i(x) = \cos(x) + i\sin(x)$$

and we only want the real part (but \\(A\\) and \\(B\\) can be complex!), so we replace the imaginary exponents with trig terms and merge the constants. The imaginary part of the constants means it's possible to have $$\sin$$ terms, so we end up with

$$\lambda_1\exp(nx)\cos(cx) + \lambda_2\exp(nx)\sin(cx)$$

Now to explain the physical meaning of these. In the case of real roots, we have an exponential decay (draw it!) This is known as overdamping. The rate of decay is dependent on the constants. For repeated roots, we also have exponential decay, but it's faster than overdamping. Now these situations occur with large damping. So imagine yourself on a rusty old trampoline not getting any bounce at all. The third case, with the complex roots, is known as underdamping, and now we get our nice oscillations, along with an exponential decay. This is like a more realistic version of our example beforehand, but eventually you'll stop moving.

### Forces and Resonance

How are we able to keep bouncing? Well it turns out that by jumping, we exert a force on the trampoline that counteracts the energy lost by friction. This is known as forced oscillation. There is some driving force function acting on the oscillator. Now working through the math is long but gives interesting results. I'll explore this in another post. For trampolines the driving force is rather complicated to model (it's easier with swings).
