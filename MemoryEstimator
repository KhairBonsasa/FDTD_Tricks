import numpy as np

def estimate_memory(domain_size, discretization):
    """
    Estimate the memory required for gprMax simulation.

    Parameters:
    domain_size (tuple): Domain size in meters (length, width, height).
    discretization (tuple): Grid resolution in meters (dx, dy, dz).

    Returns:
    memory_usage (float): Estimated memory usage in GB.
    """

    # Unpack the domain and discretization values
    Lx, Ly, Lz = domain_size
    dx, dy, dz = discretization

    # Calculate the number of grid points in each dimension
    nx = int(Lx / dx)
    ny = int(Ly / dy)
    nz = int(Lz / dz)

    # Standard overhead (in bytes)
    stdoverhead = 50e6  # 50MB

    # Solid array (UInt32, 4 bytes per cell)
    solidarray = nx * ny * nz * np.dtype(np.uint32).itemsize

    # Rigid arrays (18 Int8 arrays, 1 byte per entry)
    rigidarrays = 18 * nx * ny * nz * np.dtype(np.int8).itemsize

    # Field arrays (12 Float arrays, 4 bytes per entry)
    fieldarrays = 12 * (nx + 1) * (ny + 1) * (nz + 1) * np.dtype(np.float32).itemsize

    # PML arrays (approximate contribution as 10% of the total)
    pmlarrays = 0.1 * (solidarray + rigidarrays + fieldarrays)

    # Total memory usage (in bytes)
    total_memory_bytes = stdoverhead + solidarray + rigidarrays + fieldarrays + pmlarrays

    # Convert total memory usage to GB
    total_memory_gb = total_memory_bytes / (1024 ** 3)

    return total_memory_gb

# Function to interact with the user
def get_input():
    # Ask for the domain size
    Lx = float(input("Enter the domain size in the x-direction (meters): "))
    Ly = float(input("Enter the domain size in the y-direction (meters): "))
    Lz = float(input("Enter the domain size in the z-direction (meters): "))

    # Ask for the discretization
    dx = float(input("Enter the discretization in the x-direction (meters): "))
    dy = float(input("Enter the discretization in the y-direction (meters): "))
    dz = float(input("Enter the discretization in the z-direction (meters): "))

    # Calculate memory usage
    domain_size = (Lx, Ly, Lz)
    discretization = (dx, dy, dz)
    memory_usage = estimate_memory(domain_size, discretization)

    print(f"Estimated memory required: {memory_usage:.2f} GB")

# Run the program
get_input()
