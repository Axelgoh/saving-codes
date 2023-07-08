

const Navbar = () => {
  const [isNavbarVisible, setNavbarVisible] = useState(true);

  useEffect(() => {
    let prevScrollPos = window.pageYOffset;

    const handleScroll = () => {
      const currentScrollPos = window.pageYOffset;
      const isScrolledUp = prevScrollPos > currentScrollPos;

      setNavbarVisible(isScrolledUp);
      prevScrollPos = currentScrollPos;
    };

    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  return (
    <nav className={`sidebar ${isNavbarVisible ? '' : 'hidden'}`}>
    
# saving-codes
