
With Dennard scaling hitting practical boundaries (the "Power Wall") around 2005, leading to the stagnation of CPU clock speeds at roughly 4 GHz, the question arises:

How did computational power continue to grow since then?

There is no single simple answer to this question, but one word encapsulates the primary driver responsible for the sustained, and even drastically increased, growth of computational power:
Concurrency

Definition:

    The ability of a system to progress in multiple tasks through simultaneous execution, context switching, resource sharing, and managing interactions.

Why Add More Transistors? (The Turing Paradox)

Before diving deeper into concurrency, recall that the Universal Turing Machine is theoretically capable of implementing any algorithm or program based on a sequence of instructions. Once we have a practical implementation of a linear-bounded Universal Turing Machine, we should, in principle, have no need to ever change it, as it can already carry out any task we can think of.

With this thought in mind, we might wonder: Why is Moore's Law—stating that the number of transistors on a microprocessor doubles approximately every two years—useful at all? Why would we want to modify our Turing Machine by adding more transistors if it is already "universal"?

The reason is speed and efficiency.
The definition of the Turing Machine ensures computability (can it be done?), but it does not include any notion of efficiency (how long will it take?).
We modify the machine not to make it "smarter," but to make it faster. Aside from striving for smaller transistors to increase raw switching speed, engineers have utilized the bounty of extra transistors provided by Moore's Law to make CPUs structurally more efficient.

The Rise of Concurrent Architectures

Moore's Law laid the foundation for these efforts by providing the "transistor budget" needed to add complex features. Long before the "Power Wall" was hit in 2005, concurrent computing practices were already being integrated into microprocessors to boost performance:

    Instruction Level Parallelism (ILP):
    Techniques like Pipelining and Superscalar execution, where different stages of multiple instructions (Fetch, Decode, Execute) run simultaneously on separate parts of the chip. This allows the CPU to process more than one instruction per clock cycle.

    Multithreading (Simultaneous Multithreading / SMT):
    Where a single physical CPU core is designed to handle two or more software "threads" at once. By duplicating the architectural state (registers), the CPU can switch back and forth instantly; if one thread stalls (waiting for slow memory), the other thread can jump in and use the execution units, keeping the processor busy.

    Multi-core Processors (The Post-2005 Era):
    This was the industry's direct answer to the Power Wall. Unable to make a single core faster (due to heat), engineers used the extra transistors to place multiple complete CPU cores onto a single chip. This allowed true parallel execution—running two, four, or more tasks at the exact same time—effectively multiplying performance without needing to increase the clock frequency.

